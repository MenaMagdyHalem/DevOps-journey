
# Content 
 <img src="/background.png" alt="Permissions" width="200" align="right" />

- ##### [Read and Use System](https://github.com/hossamalsankary/DevOps-journey/blob/main/linux/LinuxCommands.md#read-and-use-system-1)  
- ##### [Search For Files](https://github.com/hossamalsankary/DevOps-journey/blob/main/linux/LinuxCommands.md#search-for-files-1)
- ##### [Search inside flies](https://github.com/hossamalsankary/DevOps-journey/blob/main/linux/LinuxCommands.md#search-for-txt-inside-flies-1)
- ##### [ Evaluate and compare the basic file system features and options](https://github.com/hossamalsankary/DevOps-journey/blob/main/linux/LinuxCommands.md#evaluate-and-compare-the-basic-file-system-features-and-options)
- ##### [Archive-Backup-Compress](https://github.com/hossamalsankary/DevOps-journey/blob/main/linux/LinuxCommands.md#archive-backup-compress-unpack-and-uncompress-files)
- ##### [Create delete copy and move- files and directories](https://github.com/hossamalsankary/DevOps-journey/blob/main/linux/LinuxCommands.md#create-delete-copy-and-move-files-and-directories)







## Read and Use System

```diff
# for simple help wex can used this command -
+ ls --help

# Manual Pages With man Command
+ man ls

# Searching For Commands - apropos serching about command you don't know
+ apropos "copy file"

# Using TAB  you can used TAB to auto suggestion
+ mkd (than press TAB) >> auto suggestion will show (mkdir) command
```
- ##### Working With Files and Directories 

```diff
# show help
+ ls --help
# Listing Files and Directories
+ ls 

# Listing all
+ ls -a

# Listing all with use a long listing format and sort by file size, largest first 
+ ls -alSh

```
- ##  Move Around In The System

```diff
# The root directory in linux is  /  let's move to  root 
+ cd /

# show 
+ ls -al

# print name of curren
+ pwd

# Now move to home
+ cd /home

# Then go back again to root
+ cd ..

```
- ##### Creating Files and Directories

```diff
# Create directory  name moon 
+ mkdir moon

# Creating Files
+ touch note.txt

```
- #####  Copy and move files

```diff
! cp [source] [dest] 
# Copy File to home 
+ cp note.txt ~/

# copy the moon directory to home
+ cp -R moon ~/

# notice f to want to copy folder you have to used -R 
#  -R, -r, --recursive          copy directories recursively

# -------------------------------------------------------------

! mv [source] [dest] 
# Move Files and Directory 

+ mv note.txt ~/

# Move the moon directory to home
+ mv -R moon ~/

```

### -------------------------------------------------------------------------------------------------------------------------------------
## Search for Files
```diff
! find [/path/to/directory] [search_parameters] 
# lookup for exact name
! find [/path/to/directory] -name [name] 

+ find /bin/ -name 'ssh'

# looking for  and file contain "ss" in the first of the file name
+ find /bin/ -name '*ss'

# looking for  and file contain "ss" in the last of the file name
+ find /bin/ -name 'ss*'

# looking for file or directory with Modification time 
! find [/path/to/directory] -mmin [minute] 

# we need to do some set-up to test modification run this code
+ mkdir modification && touch modification/test modification/tus modification/ret && echo 'hello' > modification/test 

# now let's have fun
+ find modification/ -mmin 1  #get all files that last modified in Exactly  1 minute
+ find modification/ -mmin -1  #get all files that last modified between now and last 1 minute
+ find modification/ -mmin +1  #get all files that last modified before   1 minute

! notice 
! Modification = Create or Edit
! Modified Time != Change Time

+  find modification/ -mtime 2

# Change Time
+  find modification/ -cmin 2 


# Search ParametersModified Time

# Search Parameters – File Size
! find -size [size]

! c bytes
! k kilobytes
! M megabytes
! G gigabytes

# Exactly 512 kb
+ find -size 512k 

# Greater than 512 kb
+ find -size +512k 

+ find -size -512k # Less than 512 kb
# Search for file name != test
+ find  modification/ -type f -not -name "test" 


! Permissions: 664 = u+rw,g+rw,o+r
# find files with exactly 664 permissions
+ find /usr/bin/ -perm 664

# find files with at least 664 permissions
+ find /usr/bin/ -perm -664

# find files with any of these permissions
+ find /usr/bin/ -perm /664

# find files with exactly 664 permissions
+ find /usr/bin/ -perm u=rw,g=rw,o=r

# find files with at least 664 permissions
+ find /usr/bin/ -perm –u=rw,g=rw,o=r

# find files with any of these permissions
+ find /usr/bin/ -perm /u=rw,g=rw,o=r
```
### -------------------------------------------------------------------------------------------------------------------------------------
## Search for txt inside flies
 - ###### Searching With Grep
 ```diff 
 ! grep [options] ‘search_pattern’ file

 # if you are using CentOS Linux  try this
 + grep 'CentOS' /etc/os-release
 
 # with --ignore-case or -i  now  ignore case distinctions
  + grep --ignore-case 'CentOS' /etc/os-release

 # with  --recursive  or -r  search in all files inside directories
  + grep --recursive   'CentOS' /etc/

 # with --invert-match  or -v       select non-matching lines
  + grep --invert-match  'CentOS' /etc/os-release

 # with -w, --word-regexp         force PATTERN to match only whole words
 grep --word-regexp  'CentOS' /etc/os-release

 ```
 - ###### Analyze Text With Regular Expressions

 ```diff
# ^ “The line begins with”
+ grep -i '^CentOS' /etc/os-release

# $ “The line ends with”
+ grep  -e '"' /etc/os-release

# . “Match any ONE character”
+ grep   'ce.t' /etc/os-release

# result going to be like this centos >> with . any character could be 
+ grep  -wr 's.h' /etc/

# *: Match The Previous Element 0 Or More Times in this example we tell grep if you found last character its grep it if not grep the word match with "le"
+ grep -r 'let*' /etc/

#'egrep' means 'grep -E'.
# {}: Previous Element Can Exist “this many” Times
! 0{min,max}
 
+ egrep -r '0{3,}' /etc/
! or
+ grep -Er '0{3,}' /etc/

# ?: Make The Previous Element Optional
+ egrep -r 'centos?' /etc/

# {}: Previous Element Can Exist “this many” Times
+ egrep -r '0{3,5}' /etc/ 

# |: Match One Thing Or The Other
+ egrep -ir 'enabled?|disabled?' /etc/

# []: Ranges Or Sets
+ egrep -r 'c[au]t' /etc/
+ egrep -r '/dev/.*' /etc/
+ egrep -r '/dev/[a-z]*[0-9]' /etc/

  ```
  #### -------------------------------------------------------------------------------------------------------------------------------------

  ## Evaluate and compare the basic file system features and options
- ##### Compare and manipulate file content diff 
```diff 
#- Compare file1 and file 2
> diff file1 file2 

# Compare file1 and file 2 with output in two columns
> diff -y file1 file2 

# result   !file1!                              !file2!
! hello linux / hello aws		 			      |	hello linux / hello world

```
- ##### Filter adjacent matching lines from file

```diff 
# we have file has a lot of repeated  data and you want to filter it
> uniq file > newuniqfile - Remove equal consecutive rows

#Remove equal consecutive rows comparing only first two characters
> uniq -w 2 fle -

#Remove equal consecutive rows and show number of occurrences
> uniq -c file  
```
- ##### Filter and order file content
```diff
#Write sorted concatenation of all FILE
> sort file

#ignore leading blanks
> sort -b file
 ```

 - ##### Print selected parts of lines from each  FILE to standard output.
```diff 
#  -d, --delimiter
# -d, --delimiter
# run this command in your terminal to
! echo "hello from linux terminal" > file

> cut -d " " -f 1,3 file
# result 
! hello


> cut -d " " -f 1,3 file

#result 
! hellp linux


```
- #### show the content of file on your terminal
```diff 
# display the content of file
> cat fi

# --number-nonblank
> cat -b file

# Print first 10 file lines
> head file

# Print first 2 file lines
> head -n 2 file

> head -n 3 /etc/os-release 

## Print last 10 file lines
> tail -n 2 file

> tail -n 3 /etc/os-release 

```
- #### tr translate set of characters one to set of characters two

```diff 
> echo "hellp hossam" | tr " " _
#result 
! hellp_hossam

> echo "hellp Dhossam" | tr --delete [:lower:]
#result 
! D

> echo "hellp Dhossam" | tr --delete [:blank:]
#result
! hellpDhossam
```
- ##### sedd
-  Sed is a stream editor.  A stream editor is used to  per‐
       form  basic  text  transformations  on an input stream (a
       file or input from a pipeline).  While in some ways simi‐
       lar  to  an  editor which permits scripted edits (such as
       ed), sed works by making only one pass over the input(s),
```diff 
# sed - Without -i the results of file alteration won't be permanent
> sed " " file path
# change all the words javascript to go on the flay this not will be effective to the file
> sed "s/javascript/go/" ~/test_file  

# change all the words javascript to go on the flay this not will be effective to the file
> sed "s/javascript/go/" ~/test_file  

# make this change permanent 
> sed -i "s/javascript/go/g" ~/test_file  

# file - For row 10, it will change first occurrence of source to target. Print all rows.
>  sed "10si/javascript/go/g" ~/test_file 

!important 
# if you want  to delete all word javascript 
> sed "/javascript/" ~/test_file 


```
 ## Archive, backup, compress, unpack, and uncompress files
 - ##### tar - Save many files into a single file.
 ```diff 
#crate tar file 
tar cf file.tar *

#list active 
> tar --list --file   file.tar
> tar tfv file.tar

# extract tar 
tar xf file.tar

# with gzip 
tar czvf file.tar.gz *

#list active 
> tar --list --file   file.tar.gz 
> tar tfv  file.tar.gz  

# extract tar 
> tar xf file.tar

 ```
 ##  Create, delete, copy, and move files and directories

```diff 
#create file
> mkdir test 

#with -p you can create  directory inside directory 
> mkdir -p mi/ch/test 

#touch file 
> touch test-file

# Remove file 
> rm file_name

# Remove directory  with a notify before delete
> rm --recursive  directory

# without any notify -rf
> rm --recursive --force   directory

#copy and remove
> cp file ~/home
 
# directory to home -rf
> cp --recursive --force  ./test ~/home

#move and remove
> mv file ~/home
 
# move directory to home -rf
> mv --recursive --force  ./test ~/home
```


