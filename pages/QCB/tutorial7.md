---
layout: page
author: Gianfranco Abrusci
mathjax: true
---
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>


We obtained the following setup:
<IMG class="displayed" src="../../img/tut5/setup.png" alt="" width="500" height="500">


## Running the simulation
We are ready to launch the simulation.

<p class="prompt prompt-attention">Check each conf file individually
to check that every command is properly defined </p>

For this system, we will follow several steps.

# First step
We need to equilibrate the lipidic tails with `*-01.conf` in NVT.

<p class="prompt prompt-attention">Modify the PME</p>
<p class="prompt prompt-attention">Is there something you have never seen?</p>
<p></p>
We should tell _NAMD_ what to keep fixed.

<p class="prompt prompt-question">Let's make sense
of the errors we have.</p>

# Second step
We will restart the simulation and let everything move,
but for the protein that will be harmonically restraints.
The aim is to let the membrane close the gap with the protein.

We will use the `tcl` script `keep_water_out.tcl` to expel the water
molecules that flow until the system is compact enough to prevent it.
<IMG class="displayed" src="../../img/tut5/keep_wat.png" alt="">
We can define exception for water molecules nearby the protein (the `WF`, `WCA/B/C/D`).

# Third step
We release also the protein to perform the equilibration.

# Production
Finally, we can launch the actual simulation, keeping now constant
the area of the system.

<p> </p>
<p> </p>
<p> </p>
<p> </p>
<p> </p>


Recap?[^1]

[^1]: Here the [recap](https://editor.p5js.org/Gianfree/full/Hy09u_ypX) for today tutorial.

## A new episode of...
<iframe class="center" frameborder="no" border="0" src="https://editor.p5js.org/Gianfree/embed/Sk4_1sphm" width="660px" height="260" ></iframe>

<p></p>
<p></p>
### MDFF
MDFF stands for _Molecular Dynamics Flexible Fitting_ and it is a protocol
to fit an atomistic structure into a _density map_ (see the [original paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2430731/) ).

The need for this kind of procedure arises from the increase in the cryo-em structures, for which there is a database similar to the Protein Data Bank,
the [Cryo-EM database](http://www.emdatabank.org/).

To achieve the wanted fitting several techniques could be employed; the _rigid-body_
docking; the _flexible fitting approach_, where the macromolecule is divided into rigid
pieces that are rigid-body docked and optimized with some refinement; elastic network models.

In this tutorial we will take advantage of the MD power to improve the _flexible fitting_
that can be obtained by other software (see the [reference article](https://www.sciencedirect.com/science/article/pii/S1046202309000887?via%3Dihub) on MDFF).



The implementation of MDFF requires a modified potential for our simulation:
<p align="center">
$$
U = U_{MD}  +  U_{CRYO-EM} + U_{SecStruct}
$$
</p>
where $$U_{MD}$$ is the usual ff, $$U_{SecStruct}$$ preserves the secondary structure
and avoid the introduction of wrong chirality, and/or cispeptide bonds.
The key part is related to the $$U_{CRYO-EM}$$:

$$
U_{CRYO-EM}(\{\vec{r}_i\}) = \sum_j w_j V_{CRYO-EM}(\vec{r}_j)
$$

with $$w_j$$ is a weight for each atom, and

$$
V_{CRYO-EM} =
\begin{cases}
  \xi \big[1 - \frac{\Phi(\vec{r}) - \Phi_{thr}}{\Phi_{max} - \Phi_{thr}}\big] &\quad\text{if } \Phi(\vec{r})\ge \Phi_{thr} \\
  \xi &\quad\text{if } \Phi(\vec{r})\lt \Phi_{thr} \\
\end{cases}
$$

with $$\xi$$ a scaling factor, and $$\Phi(\vec{r})$$ is the data of the CRYO-EM in a given voxel.
For $$\Phi_{max}$$ and $$\Phi_{thr}$$, look at the big screen.

For this tutorial you can download the necessary [files](https://www.ks.uiuc.edu/Training/Tutorials/science/mdff/mdff-tutorial-files.tar.gz) and the [instructions](https://www.ks.uiuc.edu/Training/Tutorials/science/mdff/tutorial_mdff.pdf) for the TCBG group in Urbana-Champaign.


# Notes
