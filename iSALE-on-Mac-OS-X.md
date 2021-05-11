## macOS 10.13 (High Sierra)

With the move to High Sierra, `gcc4.9` is no longer supported. The method described here installs `gcc7` and is sufficient to get `iSALE` and `pySALEPlot` working on your High Sierra mac. 

Note: I have not tried to install `vimod` (cannot get `qt3` to work with `gcc` versions 5 and above) or `iSALEPlot` (as it is obsolete now we have `pySALEPlot`)

### Install Xcode from the mac app store

###  Install the command line tools: 

<pre>xcode-select --install</pre>

###  Migrate MacPorts

If you have an existing MacPorts installation, follow the migration guidelines here: https://trac.macports.org/wiki/Migration

* Install MacPorts base for 10.13 High Sierra from here: https://www.macports.org/install.php
* (Optional) generate a list of your installed ports, so you can reinstall them all later, if required (e.g. `port -qv installed > myports.txt`)
* Remove all installed ports:
    
<pre>
sudo port -f uninstall installed
sudo port clean all
</pre>

### Install XQuartz 

Download and install XQuartz from here: http://xquartz.macosforge.org/landing/

You will need to logout and back in again after this.

### Install `python` from MacPorts (for `pySALEPlot`):
 
Here we'll also install some necessary packages for `pySALEPlot` to work. `ipython` is not necessary, but recommended.
<pre>
sudo port install python27
sudo port select --set python python27
sudo port install py27-matplotlib
sudo port install py27-numpy
sudo port install py27-scipy
sudo port install py27-ipython
</pre>

Note that if the version of `matplotlib` you install is lower than 2.1.1, then you will also need to install `tkinter`:

<pre>
sudo port install py27-tkinter
</pre>

### Install gcc

First install `gcc`. As of Nov 2017, this installs `gcc 7.2.0`, which seems to work fine for iSALE.

<pre>
sudo port install gcc7
</pre>

Tell your mac to use this `gcc` version and not the Xcode version.

<pre>
sudo port select --set gcc mp-gcc7
</pre>

At this point, check you are using the correct version by running `gcc -v` or `gfortran -v`. It should tell you that you are using the MacPorts version here. If you see that it is the Xcode version, try selecting it again, or restarting the terminal. 

If you are installing iSALE3D, you probably want to install `openmpi` so you can run in parallel.

<pre>
sudo port install openmpi
sudo port select --set mpi openmpi-mp-fortran
</pre>

### Install MacTeX (optional: for developers wishing to edit manual)

The iSALE manual is written in LaTeX and requires `pdflatex` to compile it. Developers wishing to edit and compile an up-to-date manual for the trunk should install MacTeX (http://www.tug.org/mactex/index.html). Note this is a large package and is best installed over a fast network connection

### Install iSALE

At this point you should be ready to install iSALE in the [standard way](Installation-instructions#installing-isale-dellen-for-scientific-use).

## Yosemite (10.10), El Capitan (10.11) and macOS Sierra (10.12)

With the move to Yosemite, gcc 4.5 is no longer supported, so the installation instructions have changed a little to compile with gcc 4.8 or 4.9. Here is the method I used to get iSALE, vimod and iSALEPlot working on Yosemite. The same method works for El Capitan and Sierra.

### Install Xcode from the mac app store

###  Install the command line tools: 

<pre>xcode-select --install</pre>

###  Migrate MacPorts

If you have an existing MacPorts installation, follow the migration guidelines here: https://trac.macports.org/wiki/Migration

* Install MacPorts base for 10.10 Yosemite from here: https://www.macports.org/install.php
* (Optional) generate a list of your installed ports, so you can reinstall them all later, if required
* Remove all installed ports:
    
<pre>
sudo port -f uninstall installed
sudo port clean all
</pre>

### Install XQuartz 

Download and install XQuartz from here: http://xquartz.macosforge.org/landing/

You will need to logout and back in again after this.

### Install python from MacPorts (for pySALEPlot):
  
<pre>
sudo port install python27
sudo port select --set python python27
sudo port install py27-matplotlib
sudo port install py27-numpy
sudo port install py27-scipy
</pre>

### Install pgplot from MacPorts (only required if installing iSALEPlot):

Note, installing pgplot before gcc means that gcc 4.9 (gcc49) is installed by macports. This is fine, but means we need to make a small fix to qt3 (see step 9). 
(also note, when Yosemite was first released (~Oct 2014), this step installed gcc 4.8. As of Jan 2015, it installs gcc 4.9. Both seem to work equally well).

<pre>
sudo port install pgplot
</pre>

### Select the MacPorts gcc compiler 

This step is necessary, otherwise the Xcode version will be used, and this causes lots of problems later.

<pre>
sudo port select --set gcc mp-gcc49
</pre>
  
At this point, check you are using the correct version by running `gcc -v` or `gfortran -v`. It should tell you that you are using the MacPorts version here. If you see that it is the Xcode version, try selecting it again, or restarting the terminal. 

### Install qt3 (for vimod)

Now we have gcc, we need to install qt3. The best way (and the only way supported by the iSALE development team) is to do this through MacPorts:

<pre>
sudo port install qt3
</pre>

Because we are using gcc49, there is a bug in qt3, which is unlikely to ever get fixed upstream. So, we have to do it by hand here. Edit the file ‘qvaluelist.h’ in /opt/local/include/qt3 (assuming your MacPorts is installed in the standard location), using your favourite text editor:

<pre>
sudo vim /opt/local/include/qt3/qvaluelist.h
</pre>

and add the line:

<pre>
#include <stddef.h>
</pre>

to the header. I did this after the line `#define QVALUELIST_H`. I’m not sure how important its placement is, but that worked for me

### Install other optional packages

You may also want to install `gnuplot` and `openmpi` (for all tests to pass).

<pre>
sudo port install gnuplot
sudo port install py27-ipython
sudo port install openmpi
sudo port select --set mpi openmpi-mp-fortran
</pre>

### Install MacTeX (optional: for developers wishing to edit manual)

The iSALE manual is written in LaTeX and requires `pdflatex` to compile it. Developers wishing to edit and compile an up-to-date manual for the trunk should install MacTeX (http://www.tug.org/mactex/index.html). Note this is a large package and is best installed over a fast network connection

### Install iSALE

At this point you should be ready to install iSALE in the [standard way](Installation-instructions#installing-isale-dellen-for-scientific-use).

## Snow Leopard (10.6), Lion (10.7) and Mountain Lion (10.8) (64-bit)

### Install Xcode 

This is not automatically installed, but should come with your Mac on the OS installation disk for 10.6.  For 10.7/8, you can install Xcode through the App Store. Once it is installed, run it once and install any updates/extensions when prompted. Finally, install the "command line utilities," from Preferences -> Downloads. Once this is installed you can close Xcode and should not need it again!

### Install Xquartz (10.7 & 10.8)

It is recommended to install this using the package here: http://xquartz.macosforge.org/landing/
I think you will need to logout and back in again after this. Mac OSX 10.6 comes with X11 pre-installed, so this step is not required.

### Install MacPorts 

Follow the instructions here: http://www.macports.org/install.php
It is recommended to install using the pkg installer for Lion/Mountain Lion

### Install remaining software using macports

To install a package using macports:

<pre>
sudo port install <package>
</pre>

where <package> is an available port (see: http://www.macports.org/ports.php) For example,

<pre>
sudo port install python27
</pre>

In some instances, where multiple versions of software exist on the machine, it may be necessary to select the correct version. After installing, the available versions can be listed with

<pre>
sudo port select --list <program>
</pre>

For example,

<pre>
sudo port select --list python
</pre>

might return

<pre>
Available versions for python:
    none (active)
    python25-apple
    python26-apple
    python27
    python27-apple
</pre>

The correct software version can then be selected with

<pre>
sudo port select <program> <version>
</pre>

For example,

<pre>
sudo port select python python27
</pre>

The following sequence of ports should install and select all the necessary software required to install and run iSALE:

GNU fortran and c compilers (required by all)

<pre>
sudo port install gcc45
sudo port select gcc mp-gcc45
</pre>

> Note: at this point it is worth verifying that the gcc compiler just installed has been correctly selected by invoking `gcc --version`.  If this command returns version number 4.2.X this may be because the `port select` command was not successful. In this case, establish where gcc is located using `which gcc`; if the result is `/usr/bin/gcc` then one solution is to remove (or rename) this link (`sudo rm /usr/bin/gcc`). At this point, `which gcc` should return `/opt/local/bin/gcc` (i.e., the macports-installed version) and `gcc --version` should return 4.5.X 

Python and supporting modules (required for pySALEPLot)

<pre>
sudo port install python27
sudo port select python python27
sudo port install py27-ipython
sudo port install py27-scipy
sudo port install py27-matplotlib
</pre>

GNUplot (required for some tests and simple data output)

<pre>
sudo port install gnuplot
</pre>

PGPLOT graphics library (required for iSALEPlot)

<pre>
sudo port install pgplot
</pre>

Qt3 (required for VIMoD)

<pre>
sudo port install qt3
</pre>

openmpi for parallel simulations

<pre>
sudo port install openmpi
sudo port select mpi openmpi-mp-fortran
</pre>

### Install MacTeX (optional: for developers wishing to edit manual)

The iSALE manual is written in LaTeX and requires `pdflatex` to compile it. Developers wishing to edit and compile an up-to-date manual for the trunk should install MacTeX (http://www.tug.org/mactex/index.html). Note this is a large package and is best installed over a fast network connection

### Install iSALE

At this point you should be ready to install iSALE in the [standard way](Installation-instructions#installing-isale-dellen-for-scientific-use).

### A note about libpng

It is possible that you have a different version of libpng installed on your Mac than the one in macports. If this is the case, iSALEPlot may appear to compile ok, but then will not run, and give an error that looks something like:

<pre>
libpng warning: Application built with libpng-1.X.x but running with 1.Y.y
Segmentation fault: 11
</pre>

In this case, iSALEPlot has been build with  a different version of libpng (1.Y.y) to the version used to build the macports version of pgplot (1.X.x), and thus iSALEPlot will not work. To fix this, rerun the configure script as normal, but add the following option:

<pre>
--with-libpng=/opt/local/lib/libpng.a
</pre>

Assuming that you macports is installed to the default location (/opt/local/lib/), this should fix the problem.
