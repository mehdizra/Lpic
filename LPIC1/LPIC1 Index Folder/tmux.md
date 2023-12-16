---
tags:
  - LPIC
  - linux
  - command
  - concept
up: "[[103.5 Create, monitor and kill processes]]"
date: 2023-11-26
---
### tmux
tmux — terminal multiplexer

```bash
tmux ls # لیست تیماکس ها رو نشان میدهد
```
ctrl+b 
با این دستور به حالت کامند وارد می شویم و لیست کامندهای زیر را میتوانیم استفاده کنیم.

tmux may be controlled from an attached client by using a key combination of a prefix key, ‘C-b’ (Ctrl-b) by default, followed by a command key.

The default command key bindings are:

C-b         Send the prefix key (C-b) through to the application.
C-o         Rotate the panes in the current window forwards.
C-z         Suspend the tmux client.
!    Break the current pane out of the window.
=="    Split the current pane into two, top and bottom.==
#    List all paste buffers.
$    Rename the current session.
==%    Split the current pane into two, left and right.==
==&    Kill the current window.==
\'    Prompt for a window index to select.
(    Switch the attached client to the previous session.
)    Switch the attached client to the next session.
==,    Rename the current window.==
\-    Delete the most recently copied buffer of text.
.    Prompt for an index to move the current window.
0 to 9    Select windows 0 to 9.
==:    Enter the tmux command prompt.==
;    Move to the previously active pane.
=    Choose which buffer to paste interactively from a list.
?    List all key bindings.
D    Choose a client to detach.
L    Switch the attached client back to the last session.
\[    Enter copy mode to copy text or view the history.
]    Paste the most recently copied buffer of text.
==c    Create a new window.==
==a    attach the current client==
==d    Detach the current client.==
f    Prompt to search for text in open windows.
i    Display some information about the current window.
l    Move to the previously selected window.
m    Mark the current pane (see select-pane -m).
M    Clear the marked pane.
n    Change to the next window.
o    Select the next pane in the current window.
p    Change to the previous window.
q    Briefly display pane indexes.
r    Force redraw of the attached client.
s    Select a new session for the attached client interactively.
t    Show the time.
==w    Choose the current window interactively.==
==x    Kill the current pane.==
z    Toggle zoom state of the current pane.
{    Swap the current pane with the previous pane.
}    Swap the current pane with the next pane.
~    Show previous messages from tmux, if any.
Page Up     Enter copy mode and scroll one page up.
Up, Down
Left, Right
