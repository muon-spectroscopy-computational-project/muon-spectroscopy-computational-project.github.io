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

#### Using `pymuon-suite`'s vibrational averaging function

If `pymuon-suite` has been installed, the vibrational averaging function can be called through the command line using the command `pm-nq "vib_avg" "<parameter file>" -w`, where `<parameter file>` should be replaced with the path of the YAML file made earlier. The `-w` flag appended to the end of the command activates the write mode, removing it activates the averaging mode.

The first step is to use `pymuon-suite`'s write mode to generate a set of cell files with the selected atoms displaced along their 3 major phonon modes. This requires a CASTEP cell file and the system's phonon modes. The phonon modes can be taken from a seperate CASTEP phonon calculation. The .phonon file should have the same name as the .cell file, e.g. "muon_benzene.cell" and "muon\_benzene.phonon". Alternatively, `pymuon-suite` can use ASE to calculate the modes when it is called if the ase\_phonons parameter is set to True.

The new cell files will be split up into a file structure with a folder for each atom displaced, each containing subfolders for the modes of the respective atom which are further subdivided into folders for each grid point along that mode, like so:

```
top folder/
	  atom/
	      mode/
		  grid point/
			    molecule.cell
			    molecule.param
```

You will then need to calculate the desired property at each grid point, making sure the resulting data file is kept in the same folder as the grid point's cell file. Unfortunately, `pymuon-suite` can not yet do this automatically so you will have to write a script to set off all of the calculations.

After the property data at each grid point has been obtained, `pymuon-suite`'s averaging mode can be used to average this data. To do this, call the function as before but remove the `-w` flag. This will produce a file containing the averaged tensors of the calculated property for every atom in the system, under top\_folder/atom/molecule_tensors.dat. Additional information on the calculation may be produced and other important information depending on the property calculated. For example, if the hyperfine property is calculated then a hyperfine report will be produced detailing the hyperfine coupling constant and dipolar hyperfine components for the atom displaced and its nearest hydrogen atom (ipso hydrogen).

