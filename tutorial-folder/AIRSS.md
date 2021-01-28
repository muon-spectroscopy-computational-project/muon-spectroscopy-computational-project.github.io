## The Ab Initio Random Structure Search (AIRSS) method

The method is based on a combination of ab initio calculations, random structure searching, 
and machine learning methodologies and can -in principle- be used to predict the 
stopping site of the **paramagnetic** and **diamagnetic** muon in any type of periodic 
crystalline structure.  However, given the relatively high computational cost of 
this methodology compared to the [UEP](./UEP) methodology, it is recommended for the search of 
**paramagnetic** muon stopping sites. 

A detailed description of this methodology is given in this 
[paper by L. Liborio, S. Sturniolo and D. Jochym](https://aip.scitation.org/doi/abs/10.1063/1.5024450?journalCode=jcp). 

### Details of the software implementation

`pm-muairss` is the command line used for running this methodology. This command is first used to produce batches
of structure files with a muon defect added following a Poisson random distribution. These muonated structural
files are then optimized using CASTEP code and, then, `pm-muairss`
is used again to analyse and cluster the results of these optimizations.
 
`pm-muairss` has both a “write” and a “read” mode: one to create the batches of structure files with a 
muon defect, and the other to interpret the results of their optimization. It also needs both a structure
and a parameter file as inputs. To avoid mistakenly overwriting important data, the default mode is
read. At the moment, `pm-muairss` can take structural files from CASTEP, DFTB+ and the standard .cif files. 
The parameter files are YAML text files. A detailed description of the specific accepted 
parameters for the YAML files, and their meaning for each script, is provided [here](YAMLparameters).

An example of the work pipeline to use the AIRSS method is:

* generate a number of muonated structures with a random distribution of starting positions with `pm-muairss`
in the write mode.<br>
`pm-muairss` `-t` `w` `<structure file>` `<parameters file>` # To write<br>
This command produces a set of folders, each one containing a the structural (.cell) and parameters (.param)
CASTEP files of each of the generated muonated structures.

* relax each of these structures using the CASTEP code. This is usually done in a computer cluster 
and is the potentially computationally expensive part of the process.

* perform a cluster analysis on the relaxed structures to identify the muon stopping sites with `pm-muairss` in the read
mode.<br>
`pm-muairss` `-t` `r` `<structure file>` `<parameters file>` # To read

The `-t` `r` argument is optional; if omitted, read mode is assumed.  

The clusters with the largest number of muons are likely to be representing a muon stopping 
site in that host material.

### Example of application of the AIRSS method

#### Crystalline Silicon

The muonium stopping sites in crystalline Si are among the oldest experimentally known stopping sites.  
The stopping sites are the isotropic, tetragonal Mu<sub>T</sub> site, which is placed at the centre of 
a terahedron formed by four Si atoms, and the anisitropic, bond-centred Mu<sub>BC</sub> site, which is 
placed in one of the covalent bonds linking two Si atoms. 



The muon is located at ≈1.3 Å from its closest oxygen atom in this planar region.  A detailed description of the input and output files, resulting 
from the application of the UEP method to Fe<sub>3</sub>O<sub>4</sub>, is in this [document](supplement.pdf). 



