## iSALE on Fedora (tested for Fedora 16 and 17)

To install the packages required for iSALE:

<pre>
su -c 'yum install make gcc-gfortran gcc gcc-c++'
</pre>

To install MPI, required to run iSALE3D in parallel:

<pre>
su -c 'yum install openmpi-devel'
</pre>

Note you will need to execute the configure with `--with-mpi FCPAR=/usr/lib64/openmpi/bin/mpif90` to use MPI.

To install the visualisation software `pySALEPlot`, you need to install `numpy` and `matplotlib`

<pre>
su - c 'yum install python3-numpy python-matplotlib'
</pre>

Note you will need to configure `--with-pysalelplot` to use the pySALEPlot visualisation software.

## Optional pre-requisites

iSALE also includes two legacy visualisation tools. The prerequisites for these tools are often problematic to install, so we recommend not to install these.

To install the packages required for visualisation software (VIMoD):

<pre>

su -c 'yum install freeglut-devel  qt3-devel'
</pre>

Note you will need to configure `--with-vimod` to use the visualisation software.

To install the legacy visualisation tool, iSALEPlot, you will need PGPLOT (and gunplot):
<pre>
# install rpmfusion repositories which has pgplot in "nonfree"
su -c 'rpm -ihv http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm'
su -c 'rpm -ihv http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm'

su -c 'yum install  gnuplot pgplot-devel'
</pre>

Note you will need to configure `--with-iSALEPlot` to use this visualisation software.

To install the latex packages required to build the manual:
<pre>
su -c 'yum install texlive texlive-latex'
</pre>

### Examples of configure and make for single- and multicore CPUs

For singlecore (one cpu) you can use the following lines
<pre>
### change the prefix (directory where iSALE is installed) to whatever you want ###
./configure --prefix=/home/erik/isale --with-vimod --with-jtools --with-pysaleplot --with-qt3
make
make install
</pre>

To enable parallel computing on multicore cpus (or more than one cpu) you can use the following lines
<pre>
### change the prefix (directory where iSALE is installed) to whatever you want ###
./configure --prefix=/home/erik/isale --with-vimod --with-jtools --with-pysaleplot --with-qt3 --enable-mpi FCPAR=/usr/lib64/openmpi/bin/mpif90
make
make install

# the openmpi libraries are not in the LD_LIBRARY_PATH in Fedora 17; add them to the default search locations:
su -c 'echo -e /usr/lib64/openmpi/lib/\\n/usr/lib/openmpi/lib/ >> /etc/ld.so.conf && ldconfig'
</pre>
