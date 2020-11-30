### The Unperturbed Electrostatic Potential method

Here we present our software implementation of the Unperturbed Electrostatic Potential (UEP) Method: a method that requires only one DFT calculation, which is used to compute the electronic density of the host material. This, in turn, is used to calculate the minima of the host material’s electrostatic potential and to estimate the muon stopping site, relying on the approximation that the muon’s presence does not significantly affect its surroundings. 

The software has a complementary tool, which evaluates the interstitial high-symmetry sites in the host material that have not yet been occupied by a muon. In practice, very often, the muon stopping site will be a high-symmetry site of the crystal that has not already been occupied by another atom. Hence, the complementary tool performs a crystallographic analysis of the pure system as a useful first step. 

A detailed description of the methodology is given in this [paper by S. Sturniolo and L. Liborio](https://aip.scitation.org/doi/10.1063/5.0012381). 

#### Details of the software implementation

Both the symmetry analysis and the UEP implementation can be found in a Python library we deployed specifically to aid muon computational science: `pymuon-suite`. The library can be found on Github and is released under a GNU v3.0 open source license. 

Once installed, `pymuon-suite` provides the user both with a Python API to use for custom programs and with a series of pre-packaged scripts that perform the most common operations. Four of these scripts are relevant for finding the muon stopping site using the UEP method:
	
`pm-symmetry` performs the symmetry analysis;
	
`pm-uep-opt` performs an optimization of the muon position under the unperturbed electrostatic potential;
 	
`pm-uep-plot` produces 1D and 2D files describing the UEP along paths or on specified planes useful to produce plots; and
	
`pm-muairss` produces batches of structure files with a muon defect added following a Poisson random distribution and analyses and clusters the results of their optimization.

The symmetry script can be run simply by executing the command:

`pm-symmetry` `<structure file>`

where the structure file has to be any supported crystallographic file format (such as .cif or .cell).  

For the UEP scripts, parameter files in the YAML format are necessary. These scripts are run with the commands: 

`pm-uep-plot` `<parameters file>` 

`pm-uep-opt` `<parameters file>`
	
Finally, pm-muairss has both a “write” and a “read” mode: one to create the batches of structure files with a muon defect, and the other to interpret the results of their optimization. It also needs both a structure and a parameter YAML file as inputs. To avoid mistakenly overwriting important data, the default mode is read. The two modes are used as follows:

`pm-muairss` `-t` `w` `<structure file>` `<parameters file>` # To write 

`pm-muairss` `-t` `r` `<structure file>` `<parameters file>` # To read

The `-t` `r` argument is optional; if omitted, read mode is assumed. For the parameter files, each script has its own arguments that can be set using them. A detailed description of the specific accepted parameters for the YAML files, and their meaning for each script, is provided [here](YAMLparameters).

An example of a possible work pipeline to use the UEP method could then be as follows:

* run a CASTEP calculation on a bulk structure (non muonated) to compute the electronic density to use as input for the UEP method;

* generate a number of muonated structures with a random distribution of starting positions with pm-muairss in the write mode;

* relax each of these structures with pm-uep-opt; and

* perform a cluster analysis on the relaxed structures to identify the muon stopping sites with pm-muairss in the read
mode.

The clusters with the largest number of muons will then roughly correspond to the minima of the electrostatic potential, 
with have the largest attraction basin and are likely to be representing a muon stopping site in that host material.


#### Examples of application of the UEP method




**Example Parameter File**

```
cell_file: muon_benzene.cell
muon_symbol: H:1
atom_indices:[1, 2, 5, 49]
grid_n: 20
property: hyperfine
value_type: matrix
weight: harmonic
param_file: muon_benzene.param
```
