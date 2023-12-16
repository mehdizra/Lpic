---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[LPIC1 Sessions map of content]]"
---
you can find list of internal command by this command in shell

```bash
compgen -b
```

#### but there are some of them:

|   |   |
|---|---|
|alias|This command allows you to define commands of<br><br>your own, or replace existing ones. For example, ‘alias rm=rm -i’ will make rm interactive so you don’t delete any files by mistake.|
|break|Used mostly in shell scripting to break the<br><br>execution of a loop|
|cd|Change directory. For example, ‘cd /usr’ will<br><br>make the current directory be /usr. See also pwd.|
|continue|Used mostly in shell scripting to continue the execution of a loop|
|echo|List the value of variables, either<br><br>environment-specific or user-declared ones, but can also display a simple string.|
|export|Allows the user to export certain environment<br><br>variables, so that their values are used to all subsequent commands|
|fg|Resume the execution of a suspended job in<br><br>the foreground. See also bg.|
|history|With no arguments, gives a numbered list of<br><br>previously issued commands. With arguments, jumps to a certain number in said list.|
|kill|Send a termination signal by default, or<br><br>whatever signal is given as an option, to a process ID.|
|pwd|Print working directory|
|read|Used mostly in scripts, it is used to get<br><br>input from the user or another program|
|test|Used with an expression as an argument, it<br><br>returns 0 or 1, depending on the evaluation of said expression|
|times|Print the accumulated user and system times<br><br>for the shell and for processes run from the shell. The return status is 0.|
|type|Indicates what kind of command is the<br><br>argument taken.|
|unalias|See alias|
|wait|Usually given a process id, it waits until<br><br>said process terminates and returns its status.|