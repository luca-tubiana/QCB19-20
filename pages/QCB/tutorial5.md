---
layout: page
author: Gianfranco Abrusci
permalink: /meh_ehi
mathjax: true
---
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>


In this session we will build the setup for the KcsA, a membrane protein,
and the step to perform the simulation.

The files you need are available [here]().

[^1]: See [Membrane tutorial]() for the references.


## Recap
Find a way to make the quiz for the

## Membrane protein
We will build the setup of the KcsA, a potassium channel membrane protein.
Your setup will look like this:
<IMG class="displayed" src="../../img/tut5/setup.png" alt="" width="500" height="500">

Except from the change in the ion composition (this time KCL), we can see that
obviously we need to add a membrane patch.


## Our challenge
If we over-simplify the steps, our goal is to apply the following equation.
<IMG class="displayed" src="../../img/tut5/eq_of_love.png" alt="">
<p align="center"> The equation of love <3.</p>

<p class="prompt prompt-question">How do we go from the left side of the
equation to the right side?</p>
<p>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
</p>

The road map is:
1. Download and modify the experimental `pdb`;
2. Obtain the tetramer;
3. Create a membrane patch;
4. Insert the protein inside the membrane;
5. Solvate and ionise the sytem.

Let's see in details all the steps.

## The protein
Download from the [PDB website](https://www.rcsb.org) the entry `1K4C`.
<p class="prompt prompt-question">Have a look at the biological assembly!</p>

From the website you can already see how the protein is arranged within the membrane.

Let's open the `pdb` in _VMD_ and visualise it.

<IMG class="displayed" src="../../img/tut5/initial_pdb.png" alt="">

In this system we see that there is not only our protein (the alpha helices).
We have also water molecules, several potassium ions, few lipids and antibody
fragments that is used to crystalise the protein.
<p></p>
<p class="prompt prompt-question"> Visualise the protein secondary structure and
colour it by chain.</p>
<p></p>
<p class="prompt prompt-question">How many chain are there?</p>

Take note of the chain we need for our setup.

Let's now investigate the `pdb` file, and go and check the remarks `350`,
`465` and `470`.
<p></p>
<p class="prompt prompt-question">What do these remarks tell us?</p>
<p></p>

Now we have two pieces of information: the first one is that our system is a
tetramer (`REMARKS 350`); the second one is that we have the matrix to apply
to the system to obtain the biological assembly.

As you can see the matrix is a 3 by 4 matrix, to which we have to add a
row `{0.0 0.0 0.0 1.0}` to obtain a 4 by 4 matrix that is used by _VMD_
to apply roto-translations.

The **goal** is to create the **psf** for the tetramer. To do so, we need a
`psf` for each part of the system that is not covalently bonded to other parts.
We also need the coordinates of the system.

Let's start from the coordinates. The axis of rotation will be the _z_ axis,
and the tetramer will be built arount the `K` ions.

What we are doing here is to create 4 `pdb` files with a different `segname`.

After loading the `1K4C.pdb`, let's set an appropriate `segname` for the first
element of the tetramer (to which we will apply the identity matrix). So we just
set the segname only.

```
mol new 1K4C.pdb
set all [atomselect top all]
$all set segname A
$all writepdb KCSA-A.pdb
$all delete
```

Then we apply the second matrix to our system and we change the `segname` too.
Of course we save the system also this time.
<p class="prompt prompt-attention"> Check the new selection!</p>
```
set sel [atomselect top "all and not name K"]
$sel set segname B
$sel move { {-1.0 0.0 0.0 310.66} {0.0 -1.0 0.0 310.66}
{0.0 0.0 1.0 0.0} {0.0 0.0 0.0 1.0} }
$sel writepdb KCSA-B.pdb
$sel delete
mol delete top
```
Now we delete the structure since we change the coordinates and the matrices
are given for the given pdb.
<p class="prompt prompt-question">Complete the tetramer by applying the
other transformations.</p>




## check in cw and ions

lele

# solvating with grubmuller

# membrane patch

# orientation of the protein
As a convention, the setup has the membrane parallel to the _xy_ plane, and the
protein is aligned to the z axis.
# insertion of the protein + deletion of lipids

# solvation

# ionisation

# lipid tails

# harmonic restraints

# equilibration and production

start with membrane proteins

what to do


how to do


1. water molecules and ions


We download the pdb and we compare to the structure. Therefore  

# Configutation file
- particle mesh ewald
- short vs long range force evaluation

<IMG class="displayed" src="../../img/noimage.png" alt="" width="400" height="400">



# Notes
