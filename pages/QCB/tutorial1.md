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

### Overview

Practically, the machinery we are going to use can be exemplified
in the following way.

<IMG class="displayed" src="../../img/tut1/md_machinery.png" alt="">

In a nutshell, the ingredients we need are:
- the coordinates of the system;
- the structure of the protein, related to the force field we use;
- the force field parameters for the interactions;
- a configuration file with the appropriate settings of the used algorithms;
- a software to integrate the Newton's equations;
- the trajectory: a collection of coordinates that follow the evolution of the system.

We will rapidly see some of the files in this lesson, but
keep in mind this scheme, since it will be useful later!

# Software
Let's start from the basic. For this tutorial we will use [VMD](https://www.ks.uiuc.edu/Research/vmd/), a visualisation program
that will allow us to render pretty images and analyse our simulations as well.
The computers provided to you already have VMD installed.
If you want the software on your own laptop, you can download it from [download VMD](https://www.ks.uiuc.edu/Development/Download/download.cgi?PackageName=VMD)
with a simple registration. Choose the version `1.9.3` suitable for your operating system.


# Bash
The *Bourne Again SHell* (bash) is a command-line interpreter that allows us to execute commands via text instructions. Let's have a quick overview of the basic of `bash` in the meanwhile.

On Ubuntu type `ctrl-alt-T` in order to open a terminal. For macOS, you should find the **Terminal** in the _Applications/_ folder.
For Windows users, use the lab computers.

To check what `bash` you are using, type `which bash`. You should see something like
<p class="prompt prompt-shell">/bin/bash <br> /usr/bin/bash</p>

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

We have no interest in the `dummy_file.sh`, so we can **r**e**m**ove it with:
<p class="prompt prompt-shell">$ rm dummy_file.sh</p>
Of course, we are all smart, but in order to avoid unwanted deletion, let's add a
small command to your `~/.bashrc` (the `.` at the beginning of a filename makes it "invisible").
First, let's make a backup copy of the file:
<p class="prompt prompt-shell">$ cd #to go into the home folder <br>
$ cp .bashrc .OLD_bashrc</p>
Guess what `cp` does.

Finally we can add our line:
<p class="prompt prompt-shell">$ echo "alias rm='rm -i'" >> .bashrc </p>
If we go into `~/QCB_course` folder, create a new file and remove it, we should be
asked for confirm. Right? (Do the same on a new terminal or type `source .bashrc`)

With `bash` we can perform some basic arithmetics.
Create a new file called `my_script.sh` and open it with a text editor.
<p class="prompt prompt-attention">Try to use an editor like ViM, Emacs or nano (without a GUI)</p>

Write the following text into the file and try to understand what it does:
```bash
#!/bin/bash
i=5
for j in {1..4}
do
  echo "Adding 1 to $j: $((j + 1))"
done

echo "Math (should) work! 5*4 = $((i*j))"

```

To launch this script:
<p class="prompt prompt-shell">$ bash my_script.sh </p>
You can also launch the commands with `./my_script.sh`, if your file is an executable.
List the content of your folder and then do:
<p class="prompt prompt-shell">$ chmod 700 my_script.sh</p>
If you "list" again, did somethin change?

<p class="prompt prompt-attention"> bash is not the only shell you have on your computer! </p>

To further learn about `bash`, feel free to search it on [Google](www.google.it).

# Installing VMD (optional)
Extract the folder, run the configuration, go into the `src/` folder and install VMD.
```bash
cd Downloads/
tar xvzf VMD_something.tar.gz
cd VMD_something
./config
cd src
make install
```

Now you should be ready to go.

# Getting started

Download the [source file](). Move the `.tar.gz` archive into `QCB_course` and
untar it with
<p class="prompt prompt-shell">$ tar xvzf file.tar.gz <br>
$ rm -f file.tar.gz</p>
Now launch VMD:
<p class="prompt prompt-shell">$ vmd</p> and you should have the following:
<IMG class="displayed" src="../../img/tut1/vmd.png">
<p align="center"> VMD graphical interface.</p>

If everything works, close it and let's define a common playground.

## Easy and fast recap
There are a lot of amino acids out there.

<IMG class="displayed" src="../../img/tut1/2iolmd.jpg" alt="everywhere">

But only 20 of them are coded into our DNA. We will deal mainly with these residues,
but it is not uncommon to have acetylated residues especially in the _termini_.

"What is a _terminus_ or a residue or an amino acid?" I hear you ask.

Amino acids are the building block of proteins. If _isolated_, an amino acid
has an amine (-NH2)[^2] and a carboxyl (-COOH) group. If _linked_ with others to form
a polypeptide, they lose a hydrogen from the N-terminal (amine group) and an OH from the C-terminal (carboxyl group) and we have a residue. We will usually use **residue** without this distinction. _Ça va sans dire_, the first and the last residue have to be capped with the proper terminal end since they are not linked
from both sides.

[^2]: Under biological conditions, the N-group is protonated (-NH3+)


All amino acids have a Carbon, called carbon-alpha, where a functional group is
attached. This group is specific to each amino acid and it is called **sidechain**,
while the other (heavy) atoms, present in each residue, constitute the **backbone**.

Below we have an **Alanine** with different segments highlighted that exemplifies
the nomenclature just introduced.

<IMG class="displayed" src="../../img/tut1/src_img/recap_aminoacid.png" alt="amino_recap">
<div align="center">
a) Alanine amino acid in Licorice with the C-alpha shown. b) Residue of the same amino acid. <br>
c) Backbone (bottom) and sidechain (top).<br>
</div>


Further information will be provided as we move deep in the course.

## In media re with VMD
VMD is a software for visualising and analysing molecular systems like proteins.
We will see a small subset of the available functionality of the program.
In this lesson we will focus on the visualisation of a protein and on the basics
of a scripting language called `Tcl` (read: _tickle_).

Let's go back to the shell. In your working folder you should have the following files:
<p class="prompt prompt-shell"> 1ubq.pdb equilibration.dcd pulling.dcd ubiquitin.psf </p>

Open VMD, typing `vmd`.
We will have three windows:
1. VMD Main
2. VMD Display
3. the Terminal

In the `VMD Display` our system will be draw.
`VMD Main` is a graphical interface for all the functionality we need.

<IMG class="displayed" src="../../img/tut1/src_img/vmd_main.png" alt="">

`File`: to load molecules, render them.
`Molecule`: to perform actions on the loaded molecules.
`Graphics`: to  modify representation of the loaded structures.
`Display`: to set option for the `VMD Display`.
`Mouse`: to perform actions using the mouse.
`Extension`: contains collection of modelling and analysis tools.
`Help`: (really?).

Let's load a file containing the coordinate of a protein with the extension `.pdb`.
We will load a structure of the ubiquitin, a small protein that labels proteins that have to be degraded.
So _File -> New Molecule_ and browse `1ubq.pdb` and load it.
You will have something like this:

![ubq](../../img/tut1/1ubq.png)

Now rotate the protein. Click on the `VMD Display` and press `r` and move the mouse with the left-button pressed.
<p class="prompt prompt-question"> What if you press the right-button?</p>

You can change the center of rotation by pressing `c` and selecting an atom as pivot.
With `t` you can translate the molecule in order to better place it in the display, while with `s` you can zoom in and out (or use the scroll button). Keep on play with it!

If you lose your molecule, press `=` or go to _Display -> Reset View_.


For now we saw the protein as a bunch of lines with some red dots
overthere.
<p class="prompt prompt-question">What are these dots?</p>

Using the nomenclature defined above, we can modify what is displayed. Go to _Graphics -> Representation_ and a new window appears.

The representation style should be highlighted; if not, click on the line `Lines    Name     all`.
Then go to the _Selected Atoms_ and write `protein and backbone`.
You should have this.

![change_sel](../../img/tut1/change_select.png)

Modify the _Drawing Method_ from `Lines` to `Licorice`.
More keyword for the selections can be found if click on the _Selection_ tab.

<IMG class="displayed" src="../../img/tut1/selections.png" alt="" >
Most of the keywords will be clearer in the next lessons, so don't be scared!

As you can see, you can combine keywords with `and`, `or`, `not`.
<p class="prompt prompt-question">
What happens if you select `not protein`?</p>
The _red dots_ are water molecules whose hydrogen are not resolved by the X-rays crystallography. This is why you do not have hydrogen in your protein (the colour code for H is white).
If you change your selection into `water`, nothing should happen.

**Visualise** the protein backbone and the water.

<p class="prompt prompt-question">Does your selection work? If not, why?</p>

You can also use more complex selections! Let's make an example.

Click on the `VMD Display`, press `1` and click on a oxygen atom of water. In the `Terminal` few lines should appear. Among them
look for `index: XXX` (where `XXX` is an integer).
Go back to the _Graphical Representation_ window and use `index XXX` as _Selected Atoms_. Create a new representation (`Create Rep` button) and use the following selection:
`same residue as within 20 of (index XXX)`.

<p class="prompt prompt-question">What happens if you don't write `same residue as`?</p>


Usually proteins have a secondary structure: $$\alpha$$-helices, $$\beta$$-sheets etc... It's hard to find them if we use only sticks.
Delete all the representations you have and create a new one with
the selection `all`.
Now go to _Drawing Method_ and select _New Cartoon_.
In addition, change also the _Coloring Method_ from _Name_ into _Secondary Structure_ (we are bored by the cyan colour!). The result:
<IMG class="displayed" src="../../img/tut1/sec_str.png" alt="">

The secondary structure is inferred by the 3D arrangement of the residues and the presence of *h-bonds*, a non covalent bond between a donor (a heavy electronegative atom with a Hydrogen, usually `O-H`, `N-H`, `F-H`) and an acceptor (same kind of atoms not covalently bonded to the Hydrogen) and it is established upon geometric criteria.

Here the colouring scheme for the secondary structure.

<IMG class="displayed" src="../../img/tut1/vmd_struct.png" alt ="">     
* T = hydrogen bonded turn (3, 4 or 5 turn)
* E = extended strand in parallel and/or anti-parallel β-sheet conformation.
* B = residue in isolated β-bridge (single pair β-sheet hydrogen bond formation)
* H = 4-turn helix (α helix).
* G = 3-turn helix (3<sub>10</sub> helix)
* I = 5-turn helix (π helix)
* C = coil (residues which are not in any of the above conformations).

Now keep on playing with the colouring methods and representations. But **before** go to _Extension -> Visualization -> ViewMaster_. Click on `Create New`, so you have a representation to go back if you change too many things and you
are not pleased with it.

The choice of the settings depends on what you want to convey with your image.
Once you are happy we can (and will) do two things:
1. save our work, so we can reload the representation for future use;
2. render and save a picture.

To <u>save the representation</u>, click on _File -> Save Visualization State_, write a name for the file (usually with a `.vmd` extension) and save it.

Now quit VMD and reload the representation with _File -> Load Visualization State_.

Let's now <u>render</u>.
First of all, we need to change the backgound colour since black is not suitable for printing.
So go to _Graphics -> Colors.._ and change the _Display Backgound_ in `white`.

Then remove the axis: _Display -> Axes -> off_.

Probably your image is a bit pale. This is due to the `Depth Cueing`. Go to _Display -> Depth Cueing -> off_.
If now it is too dark, turn the cuing on again and modify the parameter in _Display -> Display Settings..._ and change the _Cueing Mode_ in `Linear`. You can also play with the related parameters.

Now if you go to _File -> Render -> Snapshot_ and _Start Render_,
 you create an image.
 Depending on your system, something will happen.

But, in general, the image has a pretty low quality. Let's improve it!

 First, in _Graphics -> Representation_ you can increase the resolution of each representation you have.
 Then, change the _Material_ in _AOChalky_.
 Finally go back to the rendering window and change the rendering engine in _Tachyon_.

<IMG class="displayed" src="../../img/tut1/render.png" alt="">


## Tcl scripting

set
puts


You can also se
<p class="prompt prompt-tk">
% display </p>

<p class="prompt prompt-tk">% display resize </p>


atomselect

for loops

alignment of the protein

## Trajectories

load equilibration
Align the Backbone
update selection


show multiple trajecotry






## Exercise

Downlod a structure from the [Protein Data Bank](https://www.rcsb.org/) and download a molecule you like (or ask for hints).

Create your custom representation of the protein, highlighting a particular residue in `Licorice`, ligands in `Licorice` or `VDW`.

## Bonus
If you manage to complete the exercise, ask for a really small task.


# Further readings
1. [VMD User's Guide](https://www.ks.uiuc.edu/Research/vmd/current/ug.pdf)


---
# Notes
