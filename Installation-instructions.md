Setting up iSALE is fairly straightforward but please read each section carefully *before* starting to follow the instructions!

## Pre-requisites

iSALE was developed primarily on a Linux and Mac OSX platform, using the GNU Fortran compiler, and a 64-bit x86-architecture. The current distribution only supports these platforms; you will need to modify certain subroutines and libraries to get iSALE working on other platforms.

The recommended platform for using iSALE is Ubuntu or Fedora.

### Instructions for installing all the necessary iSALE pre-requisites for different operating systems

* [[iSALE on Ubuntu |iSALE on Ubuntu and Debian]]
* [[iSALE on Fedora]]
* [[iSALE on Mac OS X ]]
* [[iSALE on Windows (using VirtualBox and Ubuntu)]]
* [[iSALE on CentOS]]

Under Linux, the gfortran compiler is the preferred option, but iSALE has been compiled successfully using the Intel (10.1) and Portland group compilers. 

iSALE is distributed, updated and developed using git. Please ensure that you have this package installed before proceeding and that you have familiarised yourself with how to use git.

pySALEPlot, the visualisation software accompanying iSALE, uses the PYTHON language. This is not distributed with iSALE; for information about PYTHON, visit: https://www.python.org/. pySALEPlot can be installed using the instructions [[PySALEPlot manual|here]].

The latest version of iSALE also requires several widely available additional packages to be installed prior to installing iSALE.
1. Python, NumPy, SciPy and MatPlotLib
2. qt (version 3)
For Vimod on Ubuntu the package qt3-dev-tools is needed. This is NOT availiable in the Ubuntu repositories after 12.04. The package can be found at http://packages.ubuntu.com/de/precise/qt3-dev-tools

## Installing iSALE-Dellen for scientific use

Those wishing to use iSALE as a simulation tool for science should download and use the latest stable release: iSALE-Dellen.

### Downloading iSALE-Dellen

First, download a copy of the code from the `releases` tab of the repository, or by clicking here: [iSALE-dellen](https://github.com/isale-code/iSALE2D/releases/download/dellen/iSALE2D-dellen.tar.gz). (Note, if you get an error from that link, you need to first [apply for access to iSALE](https://isale-code.github.io/access.html), and make sure you are signed into your GitHub account). 

In the terminal, go to where you downloaded the iSALE dellen release, and unpack the tarball:

    tar -xzvf iSALE2D-dellen.tar.gz

When this has finished you should see a directory `iSALE2D-Dellen` in the directory you are in.  

Change into this directory: 
<pre>
cd iSALE2D-Dellen
</pre>
the directory you are now in is known as the *iSALE-Dellen root directory*.  The contents of this directory is referred to as your *local copy of the iSALE-Dellen repository*.

### Configuring iSALE-Dellen

The next step of the installation is to configure iSALE for your specific platform and compiler. If you have not already done so, change direcry into the iSALE root directory:

<pre>
cd iSALE2D-Dellen
(or cd path/name-of-iSALE-root-directory)
</pre>

Now you want to run the `configure` program.  By default this will attempt to install iSALE and all its associated packages. 

If all of the pre-requisite packages are properly installed and you are using a supported system, `configure` should require only one argument: the path where you want the iSALE programs to be installed. Typically this will be a directory on the local disk of the machine you intend to run simulations on, e.g., `/data/isale_user/iSALE`; this directory should be *outside* your copy of the iSALE repository.

However, Users will probably wish to install visualisation software for iSALE.  To install `pySALEPlot`, a python based analysis package for use with `iSALE2D`, add `--with-pysaleplot` to the `configure` command.  To install `VIMoD` a more sophisticated visualisation tool for both 2D and 3D data, with a GUI, add `--with-vimod` to the configure command.

<pre>
./configure --prefix=/path/to/install/directory --with-pysaleplot
</pre>

Please verify that `configure` was able to set-up iSALE for all sub-projects.  A successful configure will produce output similar to:

<pre>
----------------------------------------------------------------
--------- CONFIGURATION PROCESS SUMMARY ------------------------
----------------------------------------------------------------
Version flag........................................... -DREV=1802
Make command for external packages..................... make --silent
Make flags............................................. --no-print-directory --silent
Debugging kernel enabled............................... no
Debugging libraries enabled............................ no
Profiling enabled...................................... no
Kinematic description of motion........................ EULER
Advection mode......................................... MAS
ANEOS library.......................................... ../../../ANEOS/src/libaneos.a

Fortran compiler....................................... gfortran
Fortran flags.......................................... -O3 -DREV=1802 -ffree-form
Fortran77 compiler..................................... gfortran
Fortran77 flags........................................ -O3 -DREV=1802
Fortran additional flags............................... -Dlinux -Dgfortran -DARCH_x86_64
Fortran flags for iSALE3D.............................. -DEULER -DADV_MAS -DFRONTFIX
Fortran compiler for parallel compilation.............. mpif90
Fortran compiler for iSALE-2D.......................... gfortran
Fortran flag for invocation of CPP..................... -x f95-cpp-input

C compiler............................................. gcc
C flags (debugging and optimization) .................. -O3 -DREV=1802
C++ compiler........................................... g++
C++ flags (debugging and optimization) ................ -O3 -DREV=1802
VIMoD-path............................................. ${datarootdir}/vimod

qt3 support required................................... yes
qt3 support available.................................. yes
qt3 includes........................................... -I/opt/local/include/qt3
qt3 libraries.......................................... -L/opt/local/lib -lqt-mt

OpenGL support required................................ yes
OpenGL support available............................... yes
OpenGL includes........................................ -I/usr/X11/include -I/opt/local/include
OpenGL libraries....................................... -L/opt/local/lib -lGL -lGLU

pgplot support required................................ no

f2py required.......................................... yes 
f2py available......................................... yes 
f2py compiler.......................................... f2py2.7 
f2py flags............................................. --quiet -c --fcompiler=gnu95

LaTeX required......................................... no
----------------------------------------------------------------

--------------------------------------------- DESIRED / AVAILABLE / ENABLED
iSALE-2D..................................... yes  /  yes  /  yes
iSALE-3D..................................... yes  /  no  /  no
iSALE-tests.................................. yes  /  yes  /  yes
docsrc....................................... no  /  yes  /  no
compression libraries (libjc)................ yes  /  yes  /  yes
vimod........................................ yes  /  yes  /  yes
jtools....................................... no  /  yes  /  no
tools........................................ yes  /  no  /  no
iSALEPlot.................................... no  /  yes  /  no
pySALEPlot................................... yes  /  yes  /  yes
ANEOS........................................ yes  /  yes  /  yes

everything seems to be OK - installation into.......... /Users/isale_user/iSALE/Dellen

----------------------------------------------------------------
</pre>

See the [[configure|configure options]] for more details on the configure process.  For example, if configure reports that iSALE2D/3D or any of the associated tools (pySALEPlot, vimod, jtools) are not available to install, you may need to set certain [[configure|configure options]] to manually locate required libraries. 

> Additional configuration options are explained [[configure|here]]. See also the configure-section in our [[FAQ#configure|FAQ]] for help.

### Compiling and installing iSALE-Dellen

If configuration succeeded, use following command to compile iSALE-Dellen
<pre>
make
</pre>
This command will create all the programs (subprograms and libraries) needed to run iSALE.

Note that if you are reconfiguring (e.g., after an update or with different configure options) it is prudent to make clean before recompiling:
<pre>
make clean
make
</pre>

To complete the installation of iSALE it is useful to copy all the files needed to run iSALE to a separate directory.  This is done using the command:
<pre>
make install
</pre>
This installs the binaries, libraries, manpages and documentations, example-files and much more in the path chosen by `--prefix=<...>` when starting configure.

At this point, you should add the location of the installed pySALEPlot libraries to your `PYTHONPATH`, so that they are accessible from wherever you run a pySALEPlot script from. To do this, add the following line to your ~/.bashrc file:

<pre>
export PYTHONPATH="<prefix>/lib:\${PYTHONPATH}"
</pre>

Where `<prefix>` is whatever you entered as the installation directory for iSALE-Dellen using the `--prefix` option (e.g., `/data/isale_user/iSALE`). For shells other than bash, this syntax may vary.

> Information about the installed files and the structure of the installation directory can be found [[modelsdir|here]].

### Running the demonstration simulation

iSALE is distributed with input files for a simple demonstration simulation and a number of more complex [example problems](https://github.com/isale-code/iSALE2D/wiki/Example-problems).

To run the demonstration problem after installing iSALE, go into the install directory `<prefix>` (e.g., `/data/isale_user/iSALE`) and list the contents.
<pre>
cd <prefix>
</pre>

If you explore this directory, you will find the following useful directories:

* `bin/` contains all of the iSALE executables
* `share/doc` contains iSALE documentation, including the manual (`iSALE_manual.pdf`)
* `share/eos` contains equation of state input files for iSALE
* `share/examples` contains input files for a number of [example problems](https://github.com/isale-code/iSALE2D/wiki/Example-problems)

The best example to run first is `demo2D`. To run this, go into its directory
<pre>
cd share/examples/demo2D
</pre>

And then run the iSALE2D program:

<pre>
./iSALE2D
</pre>

You should see a lot of information (about the set-up of the simulation you are running) printed to the terminal, before the following is printed:

<pre>
         SETTINGS FINISHED, START JOB
         ****************************
</pre>

The terminal will remain inactive for a few minutes while the simulation runs (unless you run iSALE in the background: `iSALE2D &`.

When the simulation ends you can visualise output of the simulation using pySALEPlot or VIMoD and compare your results with those described [here](https://github.com/isale-code/iSALE2D/wiki/iSALE-2D-demonstration).

> For advanced instructions how to use iSALE or how to setup new simulations please read the [iSALE manual](https://dx.doi.org/10.6084/m9.figshare.3473690)

### Compiling latest version of the iSALE manual

As mentioned earlier, a pdf of the manual can be found in the `share/doc` subdirectory of an iSALE installation, but this is not necessarily up-to-date.  To re-compile the manual, use the flag `--with-docsrc` during the configure step above, before compiling. 
