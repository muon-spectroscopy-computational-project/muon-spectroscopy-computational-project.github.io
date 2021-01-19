## Symmetry analysis method

Symmetry considerations are important for determining the muon stopping sites. In crystallography, the sites with high symmetry are often the preferred atomic sites. This holds true for muons as well, and in practice, very often, the muon stopping site is an intertitial high-symmetry site of the crystal. For this reason, a crystallographic analysis of the pure system that will be studied with muons is a useful first step when looking for muon stopping sites, as such analysis is significantly faster than any computer simulation. 

A detailed description of the methodology is given in this [paper by S. Sturniolo and L. Liborio](https://aip.scitation.org/doi/10.1063/5.0012381). 

### Software implementation

The symmetry analysis can be found in the Python library we deployed specifically to aid muon computational science: `pymuon-suite`. The library can be found on Github and is released under a GNU v3.0 open source license. 

Once installed, `pymuon-suite` provides the user both with a Python API to use for custom programs and with a taylored `pm-symmetry` script,  which can be used to perform the symmetry analysis.

The symmetry script can be run simply by executing the command:

`pm-symmetry` `<structure file>`

where the structure file has to be any supported crystallographic file format (such as .cif or or the CASTEP structure file .cell).  

### Example of application of the symmetry method

#### Copper 

Potential muon stopping sites in Fe<sub>3</sub>O<sub>4</sub> magnetite are  experimentally well known.  The stopping sites are:

* located within a planar region that is perpendicular to the (111) direction in the unit cell and
* situated within ≈1.5 Å of one of the oxygen atoms defining the planar region. 

The figure below show the O(111) site predicted by the UEP method: 

<img src="/images/fe3o4_muon_1.jpg" width="250" height="250" />

And this other figure below shows an example of a planar region, perpendicular to the (111) direction, which is indicated in yellow: 

<img src="/images/fe3o4_muon_2-plane.jpg" width="250" height="250" />

The muon is located at ≈1.3 Å from its closest oxygen atom in this planar region.  A detailed description of the input and output files, resulting 
from the application of the UEP method to Fe<sub>3</sub>O<sub>4</sub>, is in this [document](supplement.pdf). 
