### Vibrational averaging

#### What is vibrational averaging?

The term vibrational averaging refers to a set of methods used to approximate the effects of thermal and quantum motion of nuclei on the expectation values of properties of light atoms. These effects are highly significant for muonium. All methods involve calculating the phonon modes of a molecule and displacing the atoms along those modes. A grid of displacements is thus created for each atom desired. The desired property is then sampled at each point on the grid and averaged using some weighting. See this [paper by B. Monserrat](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.93.014302) for more information.

`pymuon-suite` implements a general, high-level vibrational averaging function that can displace an atom in a molecule along its phonon modes and then average a quantity calculated at all displacement points with any chosen weighting. Multiple atoms can be selected, allowing this process to be repeated with whatever atoms you wish to displace. This allows it to easily be extended to use many vibrational averaging methods on many physical properties.

Currently, however, only the calculation of hyperfine coupling tensors with a harmonic oscillator wavefunction as the weighting is implemented. This treats the atoms as particles in a quantum harmonic oscillator and, as such, weights the values at grid points with the wavefunction of the harmonic oscillator.

New capabilities can be implemented if you are familiar with Python and willing to implement new weighting generators and data parsers.

It should be noted that `pymuon-suite` does not displace multiple atoms simultaneously, only one at a time. Then for each atom displaced it will generate an average of the property which will have varied for all atoms due to the displacement of that one atom.

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

**Optional Parameters**

These parameters will be set to a default value if not given.

* weight: Type of weighting to be used. Currently accepted values: 
	* harmonic (harmonic oscillator wavefunction).
 
  Default: harmonic.

* param_file: Path of CASTEP .param file, which will be copied into the new file structure with the displaced cell files if specified. Default: None.

* numerical_solver: If True, solve the Schroedinger equation numerically if QLab is installed. Otherwise, solve analytically. Default: False.

* ase_phonons: If True, calculate phonon modes of the system using ASE and CASTEP. Otherwise, read in phonons from .phonon file in same directory as .cell file. Default: False.

* dftb_phonons: If True, and ase\_phonons is also True, ASE will calculate phonon modes using DFTB+ rather than CASTEP. This is much quicker but also less accurate. Brief testing has shown this to agree well with CASTEP on the direction of phonon modes and agree to within an order of magnitude for large phonon frequencies. Default: True.

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
