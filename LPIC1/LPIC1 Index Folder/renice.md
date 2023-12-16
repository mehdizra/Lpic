---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.6 Modify process execution priorities]]"
date: 2023-11-25
---
### renice
change priority of running processes by the range of numbers between (-20 to 19)
only super users can use 0 and less than 0 numbers 
renice [-n] priority [-g|-p|-u] identifier...
-g, --pgrp
-p, --pid
-u, --user

```bash
renice -n 0 -p 23423
```