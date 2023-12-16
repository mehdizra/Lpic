---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.3 Perform basic file management]]"
date: 2023-11-22
---
### cpio
copy in out
to create archive
To create a cpio archive, we use: 
``` bash
$ ls | cpio -o > archive.cpio 
```

The -o option instructs cpio to create an output. In this case, the output file created is archive.cpio. The ls command lists the contents of the current directory which are to be archived. 
To extract the archive we use : 
``` bash
$ cpio -id < archive.cpio
``` 
The -i option is used to perform the extract. The -d option would create the destination folder. The character < represents standard input. The input file to be extracted is archive.cpio