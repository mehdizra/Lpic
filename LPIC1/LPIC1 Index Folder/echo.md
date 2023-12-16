---
up: "[[103.1 Work on the command line]]"
---
send arguments to standard output 

```bash
mehdi@mvm:~$ echo salam
salam
mehdi@mvm:~$

mehdi@mvm:~$ echo -n salam # echo without \n character at the end of text
salammehdi@mvm:~$

mehdi@mvm:~$ echo -e "sa\nlam" # echo with using \n character
sa
lam

mehdi@mvm:~$ echo -ne "sa\nlam" # combine -n & -e
sa
lammehdi@mvm:~$
```