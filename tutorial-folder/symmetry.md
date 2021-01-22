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

#### TiO<sub>2</sub> rutile 

The muon stopping sites in TiO<sub>2</sub> rutile were determined by transverse field μSR measurements performed in the MUSR instrument at ISIS(UK). In the these stopping sites, the muon has a low temperature ground state and a high temperature excited state, both corresponding to a muon bound to one of the six oxygen atoms that form an octahedron around the Ti<sup>3+</sup> at the center of the TiO<sub>2</sub> rutile unit cell. Each one of these stopping sites has a different O–Ti<sup>3+</sup> bonding configuration, with the ground state formed by bonding the muon to the in-plane oxygen atoms that lie in the same plane as Ti<sup>3+</sup>. These two sites are related by symmetry and are only distinguished by the electronic structure of the TiO<sub>2</sub> rutile. 

Running `pm-symmetry` on a CASTEP TiO<sub>2</sub> rutile structural file [rutile-out.cell](/images/rutile-out.cell) produces the following output: 
`
> Wyckoff points symmetry report for rutile-out.cell  
> Space Group International Symbol: P4_2/mnm  
> Space Group Hall Number: 419  

> Absolute                                              Fractional             Hessian constraints  
> [0.         0.         1.47026712]                               [0.  0.  0.5]                 none  
> [0.         2.33609456 0.        ]                             [0.  0.5 0. ]                 none  
> [0.         2.33609456 0.73513356]             [0.   0.5  0.25]         none  
> **[0.         2.33609456 1.47026712]             [0.  0.5 0.5]            none**  
> [0.         2.33609456 2.20540069]             [0.   0.5  0.75]        none  
> [2.33609456 0.         0.        ]                             [0.5 0.  0. ]           none  
> [2.33609456 0.         0.73513356]             [0.5  0.   0.25]        none  
> [2.33609456 0.         1.47026712]             [0.5 0.  0.5]           none  
> [2.33609456 0.         2.20540069]             [0.5  0.   0.75]        none  
> [2.33609456 2.33609456 0.        ]             [0.5 0.5 0. ]           none  
`

The coordinates in bold indicate the muon stopping site that agrees with the experimental results. The predicted stopping site is shown in the figure below:

<img src="/images/rutile_muon.jpg" width="250" height="250" />


