---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.6 Modify process execution priorities]]"
date: 2023-11-25
---
### nice
set priority for commands by the range of number between (-20 to 19)
only super users can use 0 and less than 0 numbers  

```bash
nice -n 10 COMMAND
```