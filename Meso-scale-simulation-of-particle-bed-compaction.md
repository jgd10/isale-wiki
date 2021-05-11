## Description and instructions.

This simulation demonstrates how to set up iSALE to model simple planar impact experiments involving granular materials, where the individual particles are explicitly resolved. This is known as a meso-scale model. In this example, a plate impactor strikes a particle bed at 500 m/s, with a buffer plate behind the particles. The particle bed is comprised of a randomly arranged number of particles of different sizes.  The impactor, buffer plate and particles all use the same material model, but of the three materials that iSALE can track, one is used to represent the impactor and buffer, and two are used to represent particles. Hence, the particle bed is actually comprised of two (identical) particle classes. The simulation runs for 2.5 us, the time it takes the bed to be compacted.

## Running the simulation

Go to the relevant example directory
<pre>
cd <prefix>/share/examples/MesoParticles2D
</pre>

Run iSALE2D.  The simulation will take several minutes, so this should be run in the background.
<pre>
./iSALE2D -a additional.inp &
</pre>
Note that the flag `-a` tells iSALE to read in an additional input file, which contains parameters specific to the meso-scale particle set up. This file is necessary to run the simulation.

From this directory you can produce images of the simulation to visualise the material movement, pressure wave and temperature using pySALEPlot:

<pre>
python Plotting/MatPreTmp.py
</pre>

The images, which should be identical to those shown below, will be output to the directory MatPreTmp/. The pySALEPlot plotting scripts can easily be modified to generate additional images and analysis.

## Model parameters summary

The mesh is constructed using planar geometry; no extension zones are used. The grid spacing is 10 microns.

The set-up type is `MESO_PART`.

The geometry of the impactor, particle bed and buffer plate are set by:

<pre>
COL_SITE         Collision j-location          : 291
------------------- Projectile ("Object") Parameters --------------------
OBJNUM           number of objects             : 3
OBJRESH          CPPR horizontal               : 100      : 100     : 40         ! Note these define the half-height of the plate; the thickness of the plate is twice this
OBJVEL           object velocity               : -5.0D2   : 0.D0    : 0.D0
OBJMAT           object material               : matter1  : VOID___ : matter1
OBJTYPE          object type                   : PLATE    : PLATE   : PLATE
OBJTPROF         object temp prof              : CONST    : CONST   : CONST
OBJOFF_V         object vertical offset        : 0        : -200    : -280       ! This specifies the offset in number of cells from COL_SITE to the base of the object
</pre>

`COL_SITE` is required to locate the point (j-index of vertex) of collision in the mesh.

Three `PLATE` objects are required to define the impactor, particle bed and buffer plate, respectively. The first is the impactor, which has a velocity of 0.5 km/s vertically down. The second object defines the space where the particle bed will be. Note that the material for this object is defined as `VOID___`, because the particles have nothing between them; if an actual material name was specified here, the particles would be embedded in that material. The third object defines the buffer plate. It is the same material as the impactor (matter1). All the objects have the same constant temperature (300 K).  The second two objects require a vertical offset to be specified, to ensure that they are positioned correctly, relative to `COL_SITE`.

The left and right boundaries are freeslip; the top and bottom are outflow boundaries, although no material passes through either boundary during the simulation.

<pre>
------------------- Boundary Condition Parameters ----------------------
BND_L                 left                          : FREESLIP
BND_R                 right                         : FREESLIP
BND_B                 bottom                        : OUTFLOW
BND_T                 top                           : OUTFLOW
</pre>

The contents of the additional input file are important for this problem:

<pre>
#ISADD
---------------------------------------------------------------------------------------------------------------------------------------
---this is an additional input file used to specify particle classes
---------------------------------------------------------------------------------------------------------------------------------------
PARNUM       Number of particle classes        : 8
PARMAT       Material for particle class       : matter2  : matter3  : matter4  : matter5  : matter6  : matter7  : matter8  : matter9   
PARRESH      Resolution of each particle       :  5       : 5        :  5       : 5        :  5       : 5        :  5       : 5         
PARTYPE      Type of particle                  : SPHEROID : SPHEROID : SPHEROID : SPHEROID : SPHEROID : SPHEROID : SPHEROID : SPHEROID  
PARFRAC      Fractional area of particles      : 0.05     : 0.05     : 0.05     : 0.05     : 0.05     : 0.05     : 0.05     : 0.05       
PARHOBJ      Host object for particles         : 2        : 2        : 2        : 2        : 2        : 2        : 2        : 2         
PARDIST      Regular/random distribution       : RANDOM   : RANDOM   : RANDOM   : RANDOM   : RANDOM   : RANDOM   : RANDOM   : RANDOM    
PARRANGE     Size range of particles           : 0.1      : 0.1      : 0.1      : 0.1      : 0.1      : 0.1      : 0.1      : 0.1       
---------------------------------------------------------------------------------------------------------------------------------------
<<END
</pre>

* `PARNUM` specifies how many particle classes should be considered. A particle class is basically a collection of particles that have a common material, host object (see below), shape, size/size-distribution, etc.  In this problem we choose to have eight particle classes as a demonstration.

* `PARMAT` specifies the material name for each particle class

* `PARHOBJ` specifies which of the objects, defined in asteroid.inp, should act as host for the particles. In this case, all particle classes share the same host object (2), which was the one containing @VOID___@ in asteroid.inp. This implies that all particle classes will be distributed within the portion of the mesh defined by object 2.

* `PARRESH` specifies the number of cells across the diameter of the median size particle in each class. @PARRESV@ can be used to specify a different height and width for the particles.

* `PARTYPE` specifies whether the particles are SPHEROIDs or CUBOIDs.

* `PARFRAC` specifies the fractional area of the host object that should be filled with each particle class. Here we have eight particle classes, each with a PARFRAC of 0.05, that share the same host object. Hence, 40% of the mesh area defined by the host object will be filled with particles; each particle class will have an equal area of particles.

* `PARDIST` specifies whether the spatial distribution of the particles should be @REGULAR@ or @RANDOM@.

* `PARRANGE` specifies whether the particles should have a size range. If this value is zero, or not defined, all particles in the class are the same size. Non-zero values are used to specify the range in particle size, relative to the size of the median particle. Hence a value of 0.5 implies that the smallest particle is 0.5 times @PARRESH@ and the largest particle will be 1.5 times @PARRESH@. In this example, we have a @PARRANGE@ of 0.1, meaning the particles will have sizes in the range 0.9 to 1.1 times the median particle.

All other model options are standard.

## Material parameters

The material parameters are not of special importance to this demonstration. Approximate parameters for quartz are used for all three materials, but these values should not be considered accurate.

## Results

![](https://isale-code.github.io/images/examples/MesoParticles2D/000.png)
![](https://isale-code.github.io/images/examples/MesoParticles2D/001.png)
![](https://isale-code.github.io/images/examples/MesoParticles2D/002.png)
![](https://isale-code.github.io/images/examples/MesoParticles2D/015.png)
![](https://isale-code.github.io/images/examples/MesoParticles2D/028.png)
![](https://isale-code.github.io/images/examples/MesoParticles2D/031.png)
![](https://isale-code.github.io/images/examples/MesoParticles2D/040.png)