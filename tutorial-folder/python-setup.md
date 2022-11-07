### Installing the Python environment

In this tutorial we'll go through the best ways to install the python environment
on any system of your interest. The procedure changes depending on your operating
system and all of them need an internet connection.

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

