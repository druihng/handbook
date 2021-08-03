# Linux常用手册



## 文件操作



### Linux 文档操作的常用命令

```
ls, tree, cd
touch, mkdir, cp, mv, rmdir, rm 
cat, tail, head
find, whois, where ...
```



#### ls

```shell
NAME
    ls - list directory contents
SYNOPSIS
	ls [OPTION]... [FILE]...

--------------------------------------------------------------------------	
-a, --all
	  do not ignore entries starting with .
-A, --almost-all
	  do not list implied . and ..
	  
-F, --classify
        append indicator (one of */=>@|) to entries
		/*	/ 目录，@ 符号链接, *可执行文件  */		
-p, --indicator-style=slash
        append / indicator to directories		

-l      use a long listing format	

-k      like --block-size=1K		
-h, --human-readable
        with -l, print sizes in human readable format (e.g., 1K 234M 2G)
-i, --inode
		with -l, print the index number of each file
-s, --size
        with -l, print size of each file, in blocks
-S      sort by file size

-r, --reverse
        reverse order while sorting
-R, --recursive
	  list subdirectories recursively  
   
SIZE  may  be (or may be an integer optionally followed by) one of fol-
lowing: kB 1000, K 1024, MB 1000*1000, M 1024*1024, and so on for G, T,
P, E, Z, Y.
```



#### tree

```
-C 在文件和目录清单加上色彩，便于区分各种类型。
-f 在每个文件或目录之前，显示完整的相对路径名称。
-F 在执行文件，目录，Socket，符号连接，管道名称名称，各自加上"*","/","=","@","|"号。
-i 不以阶梯状列出文件或目录名称。
-L level 限制目录显示层级。
-l 如遇到性质为符号连接的目录，直接列出该连接所指向的原始目录。
-s 列出文件或目录大小。
```



#### touch

```
NAME
       touch - change file timestamps 时间戳
SYNOPSIS
       touch [OPTION]... FILE...
	   
Update  the  access  and modification times of each FILE to the current
time.

-a     change only the access time
-m     change only the modification time

-d, --date=STRING
	  parse STRING and use it instead of current time

-r, --reference=FILE
	  use this file’s times instead of current time

-t STAMP
	  use [[CC]YY]MMDDhhmm[.ss] instead of current time
```

