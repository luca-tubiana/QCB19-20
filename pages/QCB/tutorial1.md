---
layout: page
author: Gianfranco Abrusci
mathjax: true
---
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>


### Welcome to our first tutorial!

In this session we will learn the basic of visualising a protein,
play with it and a recap of what you will need.[^1]

[^1]: This tutorial is adapted from [Using VMD](https://www.ks.uiuc.edu/Training/Tutorials/vmd/vmd-tutorial.pdf)

# Software
Let's start from the basic. For this tutorial we will use [VMD](https://www.ks.uiuc.edu/Research/vmd/), a visualisation program
that will allow us to render pretty images and analyse our simulations as well.
You can download it from [download VMD](https://www.ks.uiuc.edu/Development/Download/download.cgi?PackageName=VMD)
with a simple registration. Choose the version `1.9.3` suitable for your operating system.


# Bash
The *Bourne Again SHell* (BASH) Let's have a quick overview of the basic of `bash` in the meanwhile.

On Ubuntu type `ctrl-alt-T` in order to open a terminal. For macOS, you should find the **Terminal** in the _Applications/_ folder.
For Windows users, use the lab computers.

Let's have a walk into the computer filesystem. First of all, type `pwd` (**p**rint **w**orking **d**irectory). The output should be something like:
<p class="prompt prompt-shell"> /home/your_username </p>

What is inside your folder? Type `ls` (**l**i**s**t) and read the output.
<p class="prompt prompt-question">What changes if you type "ls -lh"? (without "")</p>

Let's create now a new directory for the course.
<p class="prompt prompt-shell">$ mkdir QCB_course</p>
<p class="prompt prompt-attention">Bash does not like white spaces, so use the underscore `_`.</p>

With `pwd` we can see that we are still in the `/home` directory. Try!

Let's go inside
`QCB_course`.
<p class="prompt prompt-shell">$ cd QCB_course</p>

To create an empty file, you can use `touch dummy_file.sh`. We will see in a minute
what the extension `.sh` means.




```bash
-cd
-mkdir
cat
-ls
rm
mv
cp
echo
--variable--
.bashrc
export
alias
basic-arithmetics
```

how to launch a script
<p class="prompt prompt-shell">$ bash my_script.sh </p>
You can also launch an executable with `./my_script`. If you have a script and
you want to make it executable, do:
<p class="prompt prompt-shell">$ chmod 700 my_script.sh</p>
If you now list

<p class="prompt prompt-attention"> bash is not the only shell you have on your computer! </p>



To further learn about `bash`, feel free to search it on [Google](www.google.it)

# Installing VMD

lol

## Common Vocabulary
what is an [aminoacid]()

what is a [residue]()

C- N- terminal

atom name/sidechain/backbone

charged aminoacid- polar bubu

what is a [secondary structure]()

C-$$\alpha$$

## Getting started


# Visualising

## Images

choose representation

rendering

custom color

## Trajectories

custom color


## Tcl scripting

basic stuff in Tcl





## Summary of the codes




<p class="prompt prompt-attention"> Be careful here!</p>
<p class="prompt prompt-info"> Info </p>
<p class="prompt prompt-question"> Please answer.</p>
<p class="prompt prompt-shell"> Shell </p>
<p class="prompt prompt-tk"> tk </p>


lol

```tcl
set i 0
$i
```

```python
for i in range(10):
```


--

# Further readings

# Notes
