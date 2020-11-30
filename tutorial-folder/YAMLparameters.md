### Parameters used in the YAML input files 

Here, we list the keywords for the input files of the `pymuon- suite` scripts `pm-muairss`, `pm-uep-opt` and `pm-uep-plot`.
These keywords must be included in a file written in the YAML format, which is just a plain text file with rows written in
the format `<keyword>: <value>`

#### Unperturbed electrostatic potential optimization: `pm-uep-opt`

Here are listed all the keywords used to run the `pm-uep-opt` script, used for optimization of the muon position under 
the unperturbed electrostatic potential approximation.

* **chden_path:** path of the folder in which the charge density file produced by a CASTEP calculation (extension.den_fmt) to use
for the UEP can be found. DEFAULT:. TYPE: string;

* **chden_seed:** seedname of the charge density file produced by a CASTEP calculation (extension .den_fmt) to use for the
UEP. In combination with the previous keyword, the file willbesearchedas<chden_path>/<chden_seed>.den_fmt. DEFAULT: NONE TYPE: string;

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

* **uep_chden:** CASTEP charge density file. seed.den_fmt. DEFAULT: NONE TYPE: string;

* **uep_gw_factor:** Gaussian width factor used to define the size of the ionic charges by scaling the pseudopotential radius. DEFAULT: 5.0 TYPE: float;

* **vdw_scale:** scale factor to multiply the standard van der Waals radius of each atom in the system, used to determine the minimum distance allowed between a muon and other atoms. Bigger values will evacuate a larger sphere around the existing atoms. DEFAULT: 0.5 TYPE: float;

* **charged:** determines whether the implanted muons will be charged or neutral. Must be True to use UEP. DEFAULT: false TYPE: boolean;





