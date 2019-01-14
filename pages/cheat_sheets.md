---
layout: page
permalink: /pages/cs
---

Here you can find a small list of command you can use for `bash` and for _Vim_.
It is still work in progress, so please be kind.

# Bash

```bash
#!/bin/bash
ls
mkdir
mv
cp
pwd
man
echo
for i in {1..10}; do -commands- ; done
#this is a comment
chmod 700 filename #to make filename executable
```

# ViM
_ViM_ has 3 modes:
1. by default, when you launch ViM you are in **Normal** mode: you cannot type
words in it;
2. pressing `i` from **Normal** mode you go into **Insert** mode, and it works like a normale text editor;
3. pressing `v` from **Normal** mode, you go into the **Visual** mode.


## Normal mode

**Normal** mode is like you _home_ mode: if in doubt, press `Esc` go go back
to the **Normal** mode.

 Key    | Movement
 ---    | ---- 
 h      | move the cursor to the left
 j      | move the cursor below
 k      | move the cursor above
 l      | move the cursor to the right
 w      | move forward to the beginning of the next word
 e      | move forward to the end of the word
 b      | move backward to the beginning of the previous word
 0      | move to the beginning of the line
 $      | move to the end of the line

You can move 3 characters on the right if you type `3l`, or
5 lines below with `5j`.

 Key    | Action
 ---    | ---- 
 y      | copy one character
 x      | cut one character
 p      | paste the character after
 d      | cut one character
 r      | replace the character (still in **NORMAL mode**)
 c      | change character (enter **INSERT mode**)
 ~      | change uppercase into lowercase and viceversa

In _Vim_ you can combine movement commands with action commands.

The order is:
`Action`_n-times_`movement`.

So, we can delete 3 characters forward with `d3l`.
