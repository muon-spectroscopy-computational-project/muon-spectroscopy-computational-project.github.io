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







