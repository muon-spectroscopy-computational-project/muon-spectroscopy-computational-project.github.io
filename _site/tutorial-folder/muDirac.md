### Prediction of frequencies and probabilities of transition between energy levels of muonic atoms

#### X-Ray Spectroscopy with negative muons

While positive muons can be used as magnetic probes acting as if they were *light protons*, negative muons have wholly different uses due to behaving in matter more as if they were *heavy electrons*. Negative muons possess the same charge and spin as electrons, and so will form bound states with nuclei that are known as muonic atoms. These atoms possess peculiar properties due to the heavier mass of the muon:

1. the muon orbitals around the nucleus are much smaller and denser than the electronic ones, meaning that the muon tends to be rather insensitive to the presence of electrons - as it is closer to the nucleus than any of them;
2. for the same reason, the orbitals can overlap significantly with the atomic nucleus, and their energy is affected by the shape of its charge distribution;
3. the orbitals have much higher binding energies, which means they can also be treated only with a relativistic theory. In classical terms, you could say the muons are 'orbiting' the nucleus at speeds close to that of light.

The consequence of these facts is that when cascading on a nucleus to form a muonic atom, muons will shed their energy in the form of highly energetic X-Ray photons, and the specific energies of these photons will be tied to the transitions between levels that are unique for each element. For this reason, muons can be [an excellent probe for non-destructive elemental analysis](https://www.sciencedirect.com/science/article/abs/pii/S0026265X1500301X?via%3Dihub). The exact characteristic energies for each element can be tabulated by experimental calibration, but they can also be derived from first principles, by solving the quantum equations to find the orbitals and their energies. However, this is not as simple as applying the usual Schrödinger equation, because as said above, the muons orbit the nucleus at relativistic energies, and the Dirac equation is necessary; plus, at these energies, the electrostatic potential itself stops being perfectly Coulombic. For these reasons, we have provided a software that easily allows one to perform these calculations by including all necessary details to achieve precision sufficient for the interpretation of experiments.

#### MuDirac

MuDirac is a simulation software that integrates the Dirac equation for muonic atoms to compute their X-Ray transition energies; it is written in C++ and can be found [on GitHub](https://github.com/muon-spectroscopy-computational-project/mudirac). Its use and functioning is extensively documented in the paper [S. Sturniolo, A. Hillier, "Mudirac: A Dirac equation solver for elemental analysiswith muonic X-rays", *X-Ray Spectrom. 2020;1–17*](https://onlinelibrary.wiley.com/doi/full/10.1002/xrs.3212), which should be cited by any work using it. Here we will give a quick tutorial on how to start using it for simple cases.

##### Installation

MuDirac uses CMake as a build system, and requires a C++ compiler. In order to compile it and prepare it to be executed on a Linux, Unix or MacOS system with a working C++ compiler installed, follow these steps:

1. download and unpack (or `git clone`) the repository on your local system;
2. within the main folder of the repository (the one containing the `README.md` file), create a subfolder called `build`;
3. within the `build` folder, run the following commands:

```bash
cmake ..
make mudirac
```

There will be now a folder `bin` containing a working compiled executable, `mudirac`. You can link or move this file wherever you need to use it.

##### Usage

MuDirac works simply by running it with an input file:

`mudirac input.in`

The input file is a text file containing rows of the form:

`keyword: value`

A full list of keywords can be found [here](https://github.com/muon-spectroscopy-computational-project/mudirac/blob/master/docs/Keywords.pdf). To learn how to use it, let's try a simple example. Open a text editor and write the following:

```
element: Au
isotope: 197
xr_lines: K1-L2,K1-L3
write_spec: T
```

Save this as `Au_basic.in` and then pass it to MuDirac. The simulation should be really fast and it should produce the files `Au_basic.xr.out`, `Au_basic.log`, `Au_basic.err` and `Au_basic.spec.dat`. The `.log` and `.err` files are just a log of the program's calculations and a file where any errors are stored; they are not important unless you're trying to figure out what went wrong in a failed calculation. The `.xr.out` file contains a text summary of the result, and the `.spec.dat` file contains tabulated data for a simulated spectrum.
Let's look at the input file and at what each line does.

`element: Au`
`isotope: 197`

This specifies that we're interested in studying gold, specifically the 197-Au isotope.

`xr_lines: K1-L2,K1-L3`

This indicates which X-ray transitions we want to know about. The notation is the IUPAC standard notation for X-ray spectrometry. These would be the transitions connecting the 1s shell (K1) to the 2p1/2 and 2p3/2 shells (L2, L3). Remember that because these orbitals are relativistic, spin-orbit coupling is built into them, and orbitals with different total angular momentum (orbital + spin) have different energies.

`write_spec: T`

Finally, this tells to the program to write also a `.spec.dat` file. Without this line, it wouldn't be created. `T` here stands for True.

Now open the `Au_basic.xr.out` file. The contents should look something like this:

```
# Z = 79, A = 197 amu, m = 206.768 au
Line    DeltaE (eV)     W_12 (s^-1)
K1-L2   1.43693e+07             4.94871e+18
K1-L3   1.48315e+07             4.63201e+18
```

The first line is a header that records the context of the calculation - the element's atomic number and atomic mass, and the mass of the particle in atomic units (for a muon this will always be 206.768 au). The next lines show for each line the transition energy in electron volts and the transition rate in 1/seconds, which connects to the relative intensity of the line in the spectrum. Generally speaking, lines with higher transition rates will be stronger, though the connection isn't perfect as there are other factors at play.

Now, this result is achieved with the default settings, that are in fact insufficient to simulate accurately an atom with a large Z like gold; as a general rule, the higher the charge of a nucleus, the more important all the additional terms. Copy `Au_basic.in` as `Au.in` and edit it to add lines so that it looks like this:

```
element: Au
isotope: 197
xr_lines: K1-L2,K1-L3
write_spec: T
nuclear_model: FERMI2
uehling_correction: T
electronic_config: Au
```

This adds three more lines:

`nuclear_model: FERMI2`

This sets the nucleus to be modelled not as a point charge, but as a Fermi 2-term charge distribution, which is far more accurate to reality. The program contains parameters for this distribution for all isotopes of interest in the periodic table. This will account for the finite size of the nucleus, and the overlap of the muon orbitals with it.

`uehling_correction: T`

This accounts for the Uehling correction, a quantum field effect relevant to electrostatics at these high energies. It can be undestood as accounting for the vacuum itself acting as a polarizable medium; because virtual electron-positron pairs can be generated in quantum field theory, these partially shield the charges and lower the traditional Coulomb force. This is an important term especially for very massive nuclei like Au or Pb and orbitals close to the nucleus.

`electronic_config: Au`

This term includes approximatively the effect of the other electrons orbiting the nucleus. It does not solve the equations for them, rather it just places them in fixed idealised orbitals and builds a negative charge background from them. The result is an additional correction to the energy, that is however tiny compared to the previous two terms, and often easily ignored.

Try running again MuDirac with this input. The calculation should take longer, and this time the output in `Au.xr.out` should be:

```
# Z = 79, A = 197 amu, m = 206.768 au
Line    DeltaE (eV)     W_12 (s^-1)
K1-L2   5.5936e+06              1.62308e+18
K1-L3   5.76294e+06             1.76987e+18
```

Note the significant changes - the energies are almost three times smaller than previously! You can try removing each of the new terms individually, or commenting them out by adding `#` at the beginning of a line, and re-running to see their effects. Now to familiarize yourself you can try a few more things:

1. try adding more `xr_lines`, for example L1-M2 and L1-M3;
2. try adding a range of lines; this can be written as K1:M5-K1:M5. It will compute all transitions within the given ranges that obey the selection rules to be allowed;
3. try plotting the spectra in the `.spec.dat` files, using Gnuplot or importing them in software like Excel or Origin.