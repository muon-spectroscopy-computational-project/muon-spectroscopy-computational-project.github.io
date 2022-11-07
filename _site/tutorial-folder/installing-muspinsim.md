### Installing `muspinsim`

In this tutorial we'll go through the best ways to install MuSpinSim on
any system of your interest, so that you can use it for the other exercises.

The first step is, of course, procuring Python itself. If you have not already
done this, see the [tutorial here](./python-setup).

#### Dependencies

`pip` will take care of installing all of the dependencies (other packages
that `muspinsim` needs to run). Just follow the instructions below.

#### Installing MuSpinSim

Granted that you already have Python and `pip` installed on your system, and a
command line ready to use, then installing `muspinsim` is easy using

```bash
pip install muspinsim --user
```
or if you are using Anaconda, you may also use

```bash
conda install muspinsim
```

and you'll be ready to go.

Alternatively if you wish to install from source, you may to get the package from
GitHub in one of two ways. If you have `git` installed and are familiar with its
use you can simply clone the repository:

```bash
git clone https://github.com/muon-spectroscopy-computational-project/muspinsim.git
```

Otherwise, you can download it as a 
[zip file](https://github.com/muon-spectroscopy-computational-project/muspinsim/archive/master.zip)
and unzip it in a folder of your choice.

To install the downloaded source, navigate to the parent directory in your
terminal. If you don't know how to do it,
[here's a handy guide for Linux and MacOS](http://linuxcommand.org/lc3_lts0020.php).
and [here's one for Windows](http://dosprompt.info/basics.asp), which has a 
different syntax. 

Once you are in the directory *above* the unzipped/cloned package, you can run:

```bash
pip install ./{package} --user
```

where `{package}` represents the name of the directory where you unzipped/cloned
the package. In your case, if you didn't rename the unzipped directory, it should be:

```bash
pip install ./muspinsim --user
```
