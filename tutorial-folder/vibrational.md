## Vibrational averaging

### What is vibrational averaging?

 Usually, the static lattice approximation is used in calculating properties of a system (e.g. in the ab initio DFT code CASTEP). This approximation assumes that all nuclei are static, classical objects whilst electrons have their quantum nature treated in full. However, for light nuclei in atoms such as muonium, quantum effects are highly important and neglecting them can produce inaccurate results. The term vibrational averaging refers to a set of methods used to approximate quantum effects on nuclei by "vibrating" the nuclei and averaging properties along those vibrations.

These methods typically involve calculating the vibrational modes of a molecule and displacing the atoms along those modes. A grid of displacements is thus created for each atom. The desired property is then sampled at each point on the grid and averaged using some weighting. See this [paper by B. Monserrat](https://journals.aps.org/prb/abstract/10.1103/PhysRevB.93.014302) for more information.

### The `pymuon-suite` implementation

`pm-nq`, the section of `pymuonsuite` relating to nuclear quantum effects, implements a general, high-level vibrational averaging function that can be extended to multiple methods and physical properties. The general workflow is as follows:

1. Calculate the phonon modes of a molecule or crystal using CASTEP or DFTB+
2. Use `pm-nq` to write out a set of structure files in which atoms are displaced from their equilibrium positions along the phonon mode eigenvectors
3. Calculate the value of the desired property at each displacement (also referred to as a grid point)
4. Use `pm-nq` to calculate an average for the property over all displacements

The following are the methods that are currently implemented and ready for use:

#### Wavefunction sampling

This method treats the muonium as an isolated particle in a 3-D harmonic oscillator. The muonium is displaced in `grid_n` increments along each of its 3 most significant phonon modes. Other atoms in the system are not displaced. The muonium can be treated like this due to its low mass relative to other chemical species, which means that its vibrations are effectively decoupled from the rest of the system. Multiple muons in the system can be selected to be displaced in this way, but they will be displaced in seperate 'runs' rather than all simultaneously. To clarify, this means that if 3 muons were selected, then 3 distinct averages could be generated, each differing from the static value due to the vibration of a single muon.

The average over the displacements will be weighted by the wavefunction of the harmonic oscillator.

#### Thermal lines

The mean value theorem for integrals can be used to show that, for a particular configuration of displacements of atoms along the phonon modes of a system, the value of a given property is equal to its vibrational average. This configuration can be approximated to by averaging over a set of "thermal lines". See the paper linked at the top of the page for more details on the background theory of thermal lines.

`pm-nq` generates a random set of thermal lines at T=0 (known as quantum points). These thermal lines each specify a set of displacements for a system, and averaging over the values calculated at each set of displacements produces an approximation to the vibrational average of a property. The more thermal lines are used, the more accurate the approximation. For each thermal line generated, its opposite is also calculated and put into the average. This cancels out odd terms in the Taylor expansion used to generate the thermal lines, increasing accuracy for relatively small computational cost.

Increasing system size should not increase the number of sampling points required for a constant level of accuracy.

### Using `pm-nq`

If `pymuonsuite` has been installed (see tutorials section), then `pm-nq` can be called from the command line. The write mode will require a YAML-format parameter file for `pm-nq`, the format and options of which are described in the parameter file section below. A CASTEP .phonon file will also be required in the same directory as the cell file, or alternatively a parameter can be set which will use ASE and DFTB+ to calculate phonons instead. If a CASTEP .param file is specified in the parameter file, it will be copied so that each displaced cell file has a matching .param file. To call the write mode enter:

```
pm-nq "vib_avg" "<parameter_file>" -w
```

where `<parameter_file>` is the path of the parameter file. This will write out a set of CASTEP .cell files with atoms displaced according to the method used. 

If the wavefunction sampling method is used, then `grid_n*3` files will be written, with the first third being displacements along the muon's first major phonon mode, the second third corresponding to the second mode and so forth. If the thermal lines method is used then `grid_n*2` files will be written, with the first half being the original randomly generated thermal lines, and the second half being their inverses.

Once the displaced cell files have been generated, you must calculate the desired quantity for each cell file, keeping the resulting data files in the same directory as the displaced cell files. The read/average mode can then be called by removing the -w tag from the write mode call:

```
pm-nq "vib_avg" "<parameter_file>"
```

This will perform the appropriate average over the data files and produce a `<name>_tensors.dat` file with the averaged quantities, alongside other files depending on the method used and property averaged over.

#### The parameter file

In order to use the vibrational averaging function, a YAML format parameter file must be created. The YAML format in this case is simply a set of entries, each on its own line, given by a parameter-value pair which are seperated by a colon. The list of required parameters is given below along with an example file.

**Mandatory Parameters**

* cell_file: Path of CASTEP .cell file, or just the filename if in working directory. If using CASTEP phonons, the .phonon file must be in this directory also.

* method: Method to be used. Currently accepted values:
	* wavefunction (wavefunction sampling)
	* thermal (thermal lines)

* muon_symbol: Symbol used to represent the muon custom species in the .cell file.

* grid_n: Number of grid points to use along each phonon mode, or number of pairs of thermal lines to generate.

* property: Property to be calculated. Currently accepted values: 
	* hyperfine (hyperfine coupling tensors.)
	* bandstructure (electronic band structure. output is currently quite messy.)

**Optional Parameters**

These parameters will be set to a default value if not given.

* selection: Array specifying which muons to displace for the wavefunction sampling mode, counting muons from 0 in the order they are in in the cell file. E.g. To select the first and third muon in the atom list, enter [0, 2]. Enter [-1] to select all muons.

  Default: [0]

* weight: Type of weighting to be used. The thermal lines method will use a uniform weighting regardless. Currently accepted values: 
	* harmonic (harmonic oscillator wavefunction for the wavefunction sampling method.)
 
  Default: harmonic.

* param_file: Path of CASTEP .param file, which will be copied with the displaced cell files if specified. 

  Default: None.

* ase_phonons: If True, calculate phonon modes of the system using ASE and DFTB+. Otherwise, read in phonons from .phonon file in same directory as .cell file. The system will first be geometry optimized using DFTB+, then its phonons will be calculated at this DFTB+ relaxed point, to ensure forces are zero. The phonon modes will then be used to displace atoms based on the input CASTEP cell file positons. This is very quick compared to CASTEP phonon calculation but is also less accurate. It will produce orthogonal phonon mode eigenvectors pointing in the right direction and eigenfrequencies of the correct order of magnitude, which renders it a good approximation for wavefunction sampling. However, this is untested with thermal lines and may not work!

  Default: False.

**Example Parameter File**

```
cell_file: muon_benzene.cell
param_file: muon_benzene.param
method: wavefunction
muon_symbol: H:1
atom_indices:[0]
grid_n: 20
property: hyperfine
weight: harmonic
```

