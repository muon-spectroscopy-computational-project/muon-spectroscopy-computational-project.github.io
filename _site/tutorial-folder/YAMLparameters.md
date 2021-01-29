### Parameters used in the YAML input files 

Here, we list the keywords for the input files of the `pymuon- suite` scripts `pm-muairss`, `pm-uep-opt` and `pm-uep-plot`.
These keywords must be included in a file written in the YAML format, which is just a plain text file with rows written in
the format `<keyword>: <value>`

#### Unperturbed electrostatic potential optimization: `pm-uep-opt`

Here are listed all the keywords used to run the `pm-uep-opt` script, used for optimization of the muon position under 
the unperturbed electrostatic potential approximation.

* **chden_path:** path of the folder in which the charge density file produced by a CASTEP calculation (extension.den_fmt) to use
for the UEP can be found. DEFAULT:./ TYPE: string;

* **chden_seed:** seedname of the charge density file produced by a CASTEP calculation (extension .den_fmt) to use for the
UEP. In combination with the previous keyword, the file will be searched as <chden_path>/<chden_seed>.den_fmt. DEFAULT: NONE TYPE: string;

* **gw_factor:** Gaussian width factor used to define the size of the ionic charges by scaling the pseudopotential radius.
 DEFAULT: 5.0 TYPE: float;
 
* **mu_pos:** starting position of the muon in the unit cell, expressed in absolute coordinates, in Å. DEFAULT: \[0.0, 0.0, 0.0\] TYPE: float;

* **geom_steps:** maximum number of geometry optimization steps. DEFAULT: 30 TYPE: int;

* **opt_tol:** force tolerance for each geometry optimization in eV/Å. DEFAULT: 1E-5 TYPE: float;

* **opt_method:** method used for geometry optimization. Corresponds to one of the methods used by Scipy’s scipy.optimize.minimize function. 
See the documentation for the options. DEFAULT: trust-exact TYPE: string;

* **particle_mass:** mass of the particle, in kg. Important for zero point energy estimation. By default, it is the mass of the muon. 
DEFAULT: 1.884E-28 TYPE: float; 

* **save_pickle:** If True,save the output result in a pickled file for further reading and reusing with other Python scripts. DEFAULT: true TYPE: boolean.
 
#### Unperturbed electrostatic potential plotting: `pm-uep-plot`

Here are listed all the keywords used to run the `pm-uep-plot` script, used for plotting the unperturbed electrostatic potential along directions and planes in the unit cell. We omit explaining the key- words chden_path, chden_seed, and gw_factor, which are in common with pm-uep-opt 

* **line_plots:** specify one or more line segments along which to plot the value of the UEP. Each line segment is specified by a list, and there are a number of possible methods to specify them:

  * crystallographic direction, starting point, length, and number of points. For example, \[\[1, 1, 0\], \[0, 0, 0\], 10, 100\]
    will produce a plot along the \[110\] direction, starting from the origin, continuing for 10 Å and with 100 points spaced 0.1 Å each;
    
  * starting point, end point, and number of points. For example, \[\[0, 0, 0\], \[1, 1, 1\], 100\] will produce a plot sampling the vector 
    connecting the origin with the position \[1, 1, 1\] Å in the cell (these are absolute positions), with a grid of 100 points;
    
  * starting atom, end atom, and number of points. For example, \[1, 2, 20\] will produce a plot sampling the line connecting the
    atoms with indices 1 and 2 in the structure file, split in 20 points.
    
* **plane_plots:** specify one or more planes along which to plot the value of the UEP. Each plane is specified by a list, and there are a number of       possible methods to specify them:

  * three corners, points along width, and points along height. For example, \[\[0, 0, 0\], \[3, 0, 0\], \[0, 0, 3\], 20, 20\] in a cubic lattice 
    with *a = 3* would produce a plot of the *xz* face of the cell, split into a 20 × 20 grid,
    
  * three atom indices to act as corners, points along width, and points along height, for example, \[0, 1, 2, 20, 20\] would produce a parallelogram
    having the vector connecting atoms 0 and 1 as base, the vector connecting atoms 0 and 2 as side, and 20 points along each side for a 20 × 20 overall grid.

#### Random structure generation: `pm-muairss`

Here are listed all the keywords used to run the `pm-muairss` script. Words that are relevant to usage with CASTEP or DFTB+ for structure optimization are included too.  

* **name:** name to call the folder for containing each struc- ture. This name will be postfixed with a unique number, e.g., struct_001. DEFAULT: struct TYPE: string;

* **calculator:** calculator(s) used to optimize the muon position. Must be a comma-separated list of values. Currently supported calculators are CASTEP, DFTB+, and UEP. Can also pass ALL as an option to generate files for all calculators. DEFAULT: dftb+ TYPE: string;

* **poisson_r:** radius in Å for generating muon sites with the Poisson disk algorithm. This radius is the minimum distance at which two muons can be placed from each other when the muonated structures are generated. DEFAULT: 0.8 TYPE: float;

* **uep_chden:** CASTEP charge density file: \<seed\>.den_fmt. DEFAULT: NONE TYPE: string;

* **uep_gw_factor:** Gaussian width factor used to define the size of the ionic charges by scaling the pseudopotential radius. DEFAULT: 5.0 TYPE: float;

* **vdw_scale:** scale factor to multiply the standard van der Waals radius of each atom in the system, used to determine the minimum distance allowed between a muon and other atoms. Bigger values will evacuate a larger sphere around the existing atoms. DEFAULT: 0.5 TYPE: float;

* **charged:** determines whether the implanted muons will be charged or neutral. Must be True to use UEP. DEFAULT: false TYPE: boolean;

* **supercell:** supercell size and shape to use. This can either be a single int, a list of three integers, or a 3 × 3 matrix of integers. For a single number, a diagonal matrix will be generated with the integer repeated on the diagonals. For a list of three numbers, a diagonal matrix will be generated where the diagonal elements are set to the list. A matrix will be used directly as is. Default is a 3 × 3 identity matrix. DEFAULT: identity TYPE: matrix;

* **out_folder:** name for the output folder used to store the structural input files generated. DEFAULT:./muon-airss-out TYPE: string;

* **geom_steps:** maximum number of geometry optimization steps. DEFAULT: 30 TYPE: int;

* **geom_force_tol:** force tolerance for each geometry optimization in eV/Å. DEFAULT: 0.05 TYPE: float;

* **clustering_method:** clustering method to use to process results. The options are `hier` (for hierarchical clustering) and `kmeans` (for k-means clustering). DEFAULT: hier TYPE: string;

* **clustering_hier_t:** normalized **t** parameter for hierarchical clustering. Higher **t** will produce a smaller number of bigger clusters. DEFAULT: 0.3 TYPE: float;

* **clustering_kmeans_k:** expected number of clusters for k-means clustering. DEFAULT: 4 TYPE: int;

* **clustering_save_min:** If True, save the minimum energy structure for each cluster as a separate file. DEFAULT: false TYPE: boolean;

* **clustering_save_format:** extension of file format in which to save the minimum energy structures if **clustering_save_min** is True. DEFAULT: .cif TYPE: string;

* **castep_command:** command used to run the CASTEP executable on the system. DEFAULT: castep.serial TYPE: string;

* **dftb_command:** command used to run the DFTB+ executable on the system. DEFAULT: dftb+ TYPE: string;

* **script_file:** path of a submission script template to copy into each individually generated structure’s folder for use with submission systems on HPC machines. Any literal instance of the string \{seedname\} will be replaced with the name of the structure in that folder, which allows us to create sub- mission scripts for batches of CASTEP structures. DEFAULT: NONE TYPE: string;

* **castep_param:** path to a CASTEP parameter file to use for all calculations. DEFAULT: NONE TYPE: string;

* **dftb_set:** Slater–Koster parameterization to use with DFTB+. It determines which elements can be treated; see dftb.org for more details. Can currently be 3ob-3-1 or pbc-0-3.DEFAULT: 3ob-3-1 TYPE: string;

* **dftb_optionals:** additional optional JSON files to activate for the DFTB+ parameterization. For example, including \<spinpol.json\> for 3ob-3-1 turns spin polarization on. Should be written like a list of strings (either in square brackets and comma separated or as a list using a as bullet and an entry on each line) DEFAULT: \[\] (empty list) TYPE: \[str\];

* **dftb_pbc:** whether to turn on periodic boundary conditions in a DFTB+ calculation. DEFAULT: true TYPE: boolean; 

* **k_points_grid:** k-points grid for periodic system calculations (CASTEP or DFTB+). Should be written like a list of integers.  DEFAULT: \[1, 1, 1\] TYPE:\[int\]; and

* **max_scc_steps:** maximum number of self-consistent steps when converging the electronic wavefunction in either CASTEP or DFTB+. DEFAULT: 200 TYPE: int;





