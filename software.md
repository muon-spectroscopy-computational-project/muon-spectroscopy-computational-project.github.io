### Software 

The MSCP develops a number of tools and packages for tackling computational challenges in muon spectroscopy. 
Here are the projects currently developed by the MSCP:

* **[pymuon-suite](https://github.com/muon-spectroscopy-computational-project/pymuon-suite)**: A collection of scripts and utilities for muon spectroscopy, containing command line tools to use alongside DFT (Density Functional Theory) simulations. These tools can be used to identify the muon stopping site(s) in a system, compute phonons, and estimate quantum effects involving the muon. The tools support external software including CASTEP and DFTB+ for performing calculations.

* **[muspinsim](/muspinsim)**: A package for simulating muon spectroscopy experiments. In particular, it simulates the spin dynamics of a system of a muon plus other spins, namely electrons and atomic nuclei. It can simulate various common experimental setups and account for hyperfine, dipolar and quadrupolar couplings. It is also able to fit its simulations to experimental data, to find the optimal parameters that describe it.

* **[mudirac](/mudirac)**: A muonic atom Dirac equation solver.

* **[Muon Galaxy](https://muongalaxy.stfc.ac.uk/)**: An open-source web platform for FAIR data analysis in muon science.
It provides a GUI for our other tools and allows users to build reproducible analysis workflows and share data and results,
without any need for prior programming experience. 
Based on the [Galaxy platform](https://galaxyproject.org).

#### External Software

The Muon Spectroscopy Computational Project (MSCP) depends on and interfaces with a wide 
range of external software. Below, there is a list of 
some of the software packages currently in use by the MSCP:

* **[The Atomistic Simulation Environment](https://wiki.fysik.dtu.dk/ase/)**:
The Atomic Simulation Environment (ASE) is a set of tools and Python modules 
for setting up, manipulating, running, visualizing and analyzing atomistic simulations
performed with many of the most popular simulation codes currently available. 

* **[Soprano](https://ccp-nc.github.io/soprano/)**:
Soprano is a Python library developed and maintained by the **[Collaborative Computational 
Project for NMR Crystallography](https://www.ccpnc.ac.uk/)**. Soprano is a software tool designed
to help scientists, who are working with crystallography and simulations, to generate, 
manipulate, run and analyse computer simulations on large data sets of crystalline structures. 
It provides a number of functionalities to help automate many common tasks in 
computational crystallography.

* **[CASTEP](http://cas-web.esc.rl.ac.uk/)**:
CASTEP is a leading code for calculating the properties of materials from first principles. 
Using density functional theory, it can simulate a wide range of properties of materials 
proprieties including energetics, structure at the atomic level, vibrational properties and 
electronic response properties. In particular, it has a wide range of spectroscopic 
features that link directly to experiment, such as infra-red and Raman spectroscopies, 
NMR, and core level spectra. `pymuno-suite` can use CASTEP simulations for predicting the muon 
stopping site. 

* **[DFTB+](https://dftbplus.org/)**:
DFTB+ is a fast, efficient and versatile quantum mechanical simulation software package.
Using DFTB+ you can carry out quantum mechanical simulations whose precision is similar 
to those of density functional theory, but which are typically around two orders of magnitude faster 
than DFT simulations. `pymuon-suite` uses DFTB+ simulations specially to treat crystalline 
organic systems.

* **[Galaxy](https://galaxyproject.org)**: an open-source platform for FAIR data analysis that enables users to:
use tools (that can be plugged into workflows) through its graphical web interface; 
run code in interactive environments (RStudio, Jupyter...);
manage data by sharing and publishing results, workflows, and visualizations; and
ensure reproducibility by capturing the necessary information to repeat and understand data analyses.
