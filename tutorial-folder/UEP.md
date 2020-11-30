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

The `-t` `r` argument is optional; if omitted, read mode is assumed. For the parameter files, each script has its own arguments that can be set using them. A detailed description of the specific accepted parameters for the YAML files, and their meaning for each script, is provided [here](https://github.com/muon-spectroscopy-computational-project/muon-spectroscopy-computational-project.github.io/blob/master/tutorial-folder/YAMLparameters.md).

#### The parameter file

In order to use the vibrational averaging function, a YAML format parameter file must be created. The YAML format in this case is simply a set of entries, each on its own line, given by a parameter-value pair which are seperated by a colon. The list of required parameters is given below along with an example file.

**Mandatory Parameters**

* cell_file: Path of CASTEP .cell file, or just the filename if in working directory.

* muon_symbol: Symbol used to represent the muon custom species in the .cell file.

* atom_indices: An array of indices of the atoms to be vibrated, counting from 1. For example, for the first 3 atoms in the system, [1, 2, 3] would be input. Enter [-1] to select all atoms.

* grid_n: Number of grid points to use along each phonon mode.

* property: Property to be calculated. Currently accepted values: 
	* hyperfine (hyperfine coupling tensors, rank matrix).

* value_type: Rank of quantity being calculated. Accepted values: matrix, vector, scalar.



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
