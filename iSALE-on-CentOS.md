## ISALE on CentOS

### CentOS 7.4

On a completely clean copy of centOS 7.4.1708, I needed to install these packages to get iSALE to configure and compile.

<pre>
sudo yum install gcc
sudo yum install gcc-gfortran
sudo yum install gcc-c++
sudo yum install python-matplotlib
sudo yum install numpy-f2py
sudo yum install git
sudo yum install make
</pre>

On CentOS 7.4.1708, this installed gcc and gfortran version 4.8.5, and python version 2.7.5.  I was then able to configure and build iSALE in the usual way.

### CentOS 6.7

To install iSALE on CentOS, there are a few prerequisites that you need to install. This is how I got iSALE to work on CentOS 6.7. I imagine similar steps could get iSALE working in RedHat.

First, install the gcc compilers:

<pre>
sudo yum install gcc
sudo yum install gcc-gfortran
sudo yum install gcc-c++
</pre>

The gcc version this installed for me was 4.4.7, which seems to work ok. You may wish to find a way to install a more recent version.

CentOS 6.7 comes with python 2.6.6 by default. For pySALEPlot, we need python 2.7. I found the easiest way to get python2.7, numpy, and matplotlib is to install anaconda from https://www.continuum.io/downloads#_unix (make sure to choose the python2.7 download, not 3.5). Then, in your downloads directory, run the following (or similar, depending on the exact downloaded filename:

<pre>
bash Anaconda2-2.5.0-Linux-x86_64.sh
</pre>

If we want to install vimod, we'll also need qt3

<pre>
sudo yum install qt3-devel
</pre>

That was sufficient to install everything needed for iSALE, pySALEPlot and vimod on a new installation of CentOS 6.7
