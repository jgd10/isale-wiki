## Essential pre-requisites

To install the packages required for iSALE:

    sudo apt-get install build-essential gfortran g++ 

To install the packages required for the pySALEPlot visualisation software:

    sudo apt-get install libpng-dev python python-numpy python-scipy python-matplotlib 

Note you will need to configure `--with-pysaleplot` to use pySALEPlot.

After installing these packages you are ready to [download and install iSALE-Dellen](https://github.com/isale-code/iSALE2D/wiki/Installation-instructions#installing-isale-dellen-for-scientific-use)

## Optional pre-requisites

iSALE also includes two legacy visualisation tools. The prerequisites for these tools are often problematic to install, so we recommend not to install these.

To install the packages required for the legacy interactive visualisation package, ViMOD:

    sudo apt-get install freeglut3-dev qt3-dev-tools

Note you will need to configure `--with-vimod` to use ViMOD. 

To install the legacy visualisation package, iSALEPlot, you will need the PGPLOT package:

    sudo apt-get install pgplot5

Note you will need to configure `--with-iSALEPlot` to use this visualisation software.


### Modifications for Ubuntu/Kubuntu 13.10 and Debian 7.x to install optional VIMoD software

The qt3-dev-tools package is not in the repositories for Ubuntu 13.10 or 14.04 ("Saucy Salamander", "Trusty Tahr") or Debian 7,x "Wheezy" or *any later versions of these Linux distributions*, but the dependency can be satisfied by installing Qt3 from source. The following has been tested on fresh Ubuntu 13.10 and Debian 7.8 installations:

1. Install all of the dependencies above besides qt3-dev-tools.

2. Install libxmu-dev:

    sudo apt-get install libxmu-dev

3. Download the Qt3 source from: http://download.qt-project.org/archive/qt/3/qt-x11-free-3.3.8.tar.gz

4. The GL, GLU, glut, and Xmu libraries are all installed to `/usr/lib/x86_64-linux-gnu`, however the Qt3 configure script will not search that directory and as a consequence disables OpenGL support. One option is to create symbolic links to the required libraries in `/usr/lib`.  A second option is to tell qmake where to find the the OpenGL libraries.  Suppose you have extracted the Qt3 files to `.../yourqt3path/`.  Now edit the file: `.../yourqt3path/mkspecs/linux-g++/qmake.conf`, and replace these lines:

```
    QMAKE_INCDIR_OPENGL    = /usr/X11R6/include
    QMAKE_LIBDIR_OPENGL    = /usr/X11R6/lib
```
with these lines:

     QMAKE_INCDIR_OPENGL    = /usr/include/x86_64-linux-gnu
     QMAKE_LIBDIR_OPENGL    = /usr/lib/x86_64-linux-gnu

5. Once the configure script is able to find the OpenGL libraries, you need to run configure and enable threading support (and optionally supply a prefix):
```
     ./configure -thread --prefix=/path/for/qt3/installation
```
Later, you may find it necessary to create this link to run VIMod successfully:
```
     sudo ln -s /path/for/qt3/installation/lib/libqt-mt.so.3 /usr/lib/libqt-mt.so.3
```
6. Make sure the output of the configure script indicates that OpenGL support is enabled.

7. Open include/qvaluelist.h and add the following near the top:
```
     #include <stddef.h>
```
8. make

_Note, if this step fails, it may be because `make` can't find the `libqt-mt.so.3` library.  In this case, try to `make install` at this point. This will fail again for the same reason, but it should have at least installed the `libqt-mt.so.3` library, so you can create the link described above (`sudo ln -s /path/for/qt3/installation/lib/libqt-mt.so.3 /usr/lib/libqt-mt.so.3`). Then try to `make` again before moving onto step 9._

9. make install

10. Checkout iSALE code and configure as, e.g.:
```
    ./configure --with-qt-includes=/home/yourname/qt3/include --with-qt-libpath=/home/yourname/qt3/lib --with-qt-binpath=/home/yourname/qt3/bin --with-vimod --with-pysaleplot --prefix=/path/for/iSALE/binaries`
```
11. make

12. make install