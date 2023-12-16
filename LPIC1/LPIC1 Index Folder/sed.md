---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.2 Process text streams using filters]]"
date: 2023-11-19
---
### sed
Sed  is a stream editor.  A stream editor is used to perform basic text
transformations on an input stream 
```bash
medme@vm1835730:~$ cat new2
ali
reza
maria
medme@vm1835730:~$ sed "s/reza/karim/" new2
ali
karim
maria
medme@vm1835730:~$ sed -i "s/reza/karim/" new2
medme@vm1835730:~$ sed "s/reza/karim/i" new2
```
to save we should use > newfile
-i : in-place , save the replace in source file
i modifier : incase sensitive 
#### Sed support Regular Expression
