### Installing `pymuon-suite` and preparing the Python environment

In this tutorial we'll go through the best ways to install the MSCP toolset on
any system of your interest, so that you can use it for the other exercises.
The procedure changes depending on your operating system. Most of the
passages are the same for Linux and MacOS systems; for Windows there are some
bigger differences. For all these procedures you will need an internet
connection.

The first step is, of course, procuring Python itself. If you already have a
Python environment set up, you can jump to the [next section](#mscp_install)

#### Preparing the Python environment

* **On Linux**: with all likelihood, Python is already installed on your system.
Congratulations! You don't have to do anything.
* **On MacOS**: Python should be present too. If necessary,
[here](https://docs.python-guide.org/starting/install3/osx/) is a handy guide
on how to install it.
* **On Windows**: our personal recommendation for an easy Python installation
on Windows is using [Anaconda](https://www.anaconda.com/download/#windows). 
It can be downloaded and ran as a graphical installer.

To check if your version of Python is working, first launch a terminal. This 
can be done on Linux and MacOS simply by finding the Terminal application in
the launch menu. On Windows, if you have decided to use Anaconda, launch
Anaconda Navigator from the menu, then
[follow these instructions](../images/anacondanav.png) to launch a terminal.

Another useful tool to have installed on your system is `pip`. `pip` is a 
package manager for Python, able to download from the internet and install 
approved Python packages in a single command. To install `pip`:

* **On Linux**: check your Software Manager application, it should be there.
Otherwise, you can install it from the command line, using a different command
depending on your distribution; for example, on Ubuntu/Debian it's

    ```bash
    sudo apt install python-pip
    ```

    and on OpenSUSE

    ```bash
    sudo zypper install python-pip
    ```

* **On MacOS**: you can install `pip` with `easy_install`:
    
    ```bash
    sudo easy_install pip
    ```

* **On Windows**: if it's not present already, you can install it from the
"Environments" tab of your Anaconda Navigator. On the right side of the tab,
select "All" packages, then type `pip` in the text field and search. Once it's
found, select it and install it.

<a name="mscp_install"></a>
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

`pip` will take care of installing most of the dependencies (other packages
that `pymuon-suite` needs to run), but one of them isn't available yet on the
Python Package Index. This is `parse-fmt`, which is used in the Unperturbed
Electrostatic Potential methods. You can clone it with `git` or download it as
a zip file as seen above, taking the corresponding URLs from [its GitHub 
repository](https://github.com/CCP-NC/parse-fmt). It is installed using the
same procedure as `pymuon-suite`.

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
the package. Do this for `parse-fmt` first and for `pymuon-suite` later. The
order is important! If `parse-fmt` is missing, the installation of `pymuon-suite`
will fail. On Linux you can also avoid this problem by simply using 
GNU Make, by entering the folder in which `pymuon-suite` is unzipped (there
should be a `Makefile`) and running:

```bash
make install-all
```

which will download and install `parse-fmt` as well.


