### Installing `pymuon-suite`

In this tutorial we'll go through the best ways to install the MSCP toolset on
any system of your interest, so that you can use it for the other exercises.

The first step is, of course, procuring Python itself. If you have not already
done this, see the [tutorial here](./python-setup).

#### Installing the MSCP tools

Granted that you already have Python and `pip` installed on your system, and a
command line ready to use, then installing `pymuon-suite` is easy. First, you
need to get the package from GitHub. You can do this in two ways. If you have
`git` installed and are familiar with its use you can simply clone
the repository:

```bash
    git clone https://github.com/muon-spectroscopy-computational-project/pymuon-suite.git
```

Otherwise, you can download it as a 
[zip file](https://github.com/muon-spectroscopy-computational-project/pymuon-suite/archive/master.zip)
and unzip it in a folder of your choice.

#### Dependencies

`pip` will take care of installing all of the dependencies (other packages
that `pymuon-suite` needs to run). Just follow the instructions below.

#### Installation

To install the downloaded packages, navigate to the parent directory in your
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
pip install ./pymuon-suite --user
```

and you'll be ready to go.


