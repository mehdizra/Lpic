---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.3 Perform basic file management]]"
date: 2023-11-22
---
### tar

```bash
tar -cvf myfile.tar file1 file2 file3 # Archive
tar -cvzf myfile.tar.gz file1 file2 file3 # Archive & compress
tar -cvjf myfile.tar.bz2 file1 file2 file3 # Archive & compress
```
-c, --create
	  Create a new archive.
-C, --directory=DIR (destination directory)
	  Change to DIR before performing any operations
-f 
	file name
-d, --diff, --compare
	  Find differences between archive and file system
--delete
	  Delete from the archive
-t, --list
	  List the contents of an archive
-r, --append
	  Append  files to the end of an archive.
-x, --extract, --get
	  Extract  files  from  an archive.
-v, --verbose
	  Verbosely list files processed.
 Compression options
-a, --auto-compress
	  Use archive suffix to determine the compression program.

-I, --use-compress-program=COMMAND
	  Filter  data through COMMAND.  It must accept the -d option, for
	  decompression.  The argument can contain command line options.

-j, --bzip2
	  Filter the archive through bzip2(1).

-J, --xz
	  Filter the archive through xz(1).

--lzip Filter the archive through lzip(1).

--lzma Filter the archive through lzma(1).

--lzop Filter the archive through lzop(1).

--no-auto-compress
	  Do not use archive suffix to determine the compression program.

-z, --gzip, --gunzip, --ungzip
	  Filter the archive through gzip(1).

-Z, --compress, --uncompress
	  Filter the archive through compress(1).

--zstd Filter the archive through zstd(1).
