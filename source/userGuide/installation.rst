Installation
============

ACQ4 depends on several free software packages to work properly.
    
* Python 2.7
* Numpy 1.7
* Scipy 0.13
* PyQt 4.8
* h5py
* Pillow (or PIL)

These are the minimal requirements to run ACQ4 (eg, for data analysis). For data acquisition, there are extra requirements:
    
* pyparsing
* pyserial (only if using serial devices--Sutter MP285, arduino, serial mice, etc)

    
You also need to make sure that the drivers for your devices are installed and working properly. 


Windows Installation
--------------------

There are two basic methods of installing ACQ4 on windows:
    
1. Download one of the .exe installers from `www.acq4.org`_; these contain a complete python distribution with all of the packages listed below. This is the quickest way to get running if you do not plan on developing new code within ACQ4. To start ACQ4, simply navigate to the entry in the start menu.

2. Prepare a complete python distribution. This is preferred if you plan to develop new code within ACQ4. All packages must match the version (2.7) and architecture (32 or 64bit) of the python version to be installed.

    * Download and install packages in order:
        * Python 2.7 (www.python.org/download)
        * PyQt4 4.10 (www.riverbankcomputing.com/software/pyqt/download)
        * NumPy-MKL 1.7 (http://www.lfd.uci.edu/~gohlke/pythonlibs/)
        * SciPy 0.13 (http://www.lfd.uci.edu/~gohlke/pythonlibs/)
        * h5py 2.2 (http://www.lfd.uci.edu/~gohlke/pythonlibs/)
        * Pillow 2.3 (http://www.lfd.uci.edu/~gohlke/pythonlibs/)
        * pyserial 2.7 (http://www.lfd.uci.edu/~gohlke/pythonlibs/)
        * PyOpenGL 3.0 (http://www.lfd.uci.edu/~gohlke/pythonlibs/)
        * PyParsing 2.0 (http://www.lfd.uci.edu/~gohlke/pythonlibs/)
    * Install git (www.git-scm.com), then clone the acq4 repository::
        
            git cone https://github.com/acq4/acq4.git
            
    * To start ACQ4, run `python -m acq4` from the source directory, or install with `python setup.py install`


Linux Installation
------------------

Linux users should install the python dependencies from their distribution's package manager. For example::

    $ sudo apt-get install python-qt4 python-qt4-gl python-qt4-sql python-pyserial python-scipy python-pyparsing python-h5py python-imaging git python2.7-dev
    
Next, clone the ACQ4 code::
    
    $ git clone https://github.com/acq4/acq4.git

Or if you prefer, install from pypi::

    $ sudo pip install acq4
    
If you wish to develop modules / devices / analysis, you will probably need a few more packages: qt4-designer pyqt4-dev-tools

To start ACQ4 run::
    
    $ python -m acq4
    

    
OSX Installation
----------------

The basic approach for OSX installation is the same as for Linux--install python dependencies from a package manager (such as homebrew), and then grab the ACQ4 source from git, pypi, or acq4.org. However, the availability of the correct packages and versions is often a confounding issue.

(detailed instructions coming soon)
