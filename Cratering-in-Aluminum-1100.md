## Description and Instructions.

This is an impact of a 6.35-mm diameter aluminium sphere into an aluminium target. The impact velocity is 7km/s. The impactor is represented by the Tillotson equation of state for Aluminium. Gravity is not considered in this calculation. No geotherm is set in the test case---the target has a constant temperature of 293K.

The model is an attempt to reproduce the aluminium validation experiments of Pierazzo et al. (2008). There are two validation tests to run into different alloys of Aluminium. This example uses Al alloy 1100-O (see also the other aluminium example using alloy [aluminum 6061](Cratering-in-Aluminum-6061)).

### Running the simulation

Go to the relevant example directory
<pre>
cd <prefix>/share/examples/aluminum_1100_2D
</pre>

Run iSALE2D.  The simulation will take several minutes, so this should be run in the background.
<pre>
./iSALE2D &
</pre>

Now, perform some postprocessing. To do this with pySALEPlot:

<pre>
python Plotting/DenPre.py
</pre>

The images, which should be identical to those shown below, will be output to the directory `DenPre/`. The pySALEPlot plotting script can easily be modified to generate additional images and analysis.

We can also use pySALEPlot to measure the crater dimensions as a function of time (using the `model.craterGrowth()` pySALEPlot function).

<pre>
python Plotting/cratergrowth.py
</pre>

This will output a figure (cratergrowth.png) which plots the iSALE crater dimensions against the experiments documented in Pierazzo et al. (2008).

To use pySALEPlot to compare this model with the [aluminum60612D](https://github.com/isale-code/iSALE2D/wiki/Cratering-in-Aluminum-6061/) example, see [[psp_plot_multiple_models|this example pySALEPlot script]]

### Model Parameters Summary.

*Model parameters for simulation.*

| DESCRIPTION                                    |  VALUE  |
| ---------------------------------------------- | ------- |
| Number of high-resolution cells in x-direction | 200     |
| Number of high-resolution cells in y-direction | 240     |
| Cell size in x-direction (m)                   | 0.15875 |
| Cell size in y-direction (m)                   | 0.15875 |
| Surface temperature (deg. Kelvin)              | 293     |
| Gravitational acceleration (m/s2)              | 0.00    |
| Projectile diameter (mm)                       | 6.35    |
| Projectile velocity (km/s)                     | 7.      |
| Projectile material (number)                   | al-1100 |

*Target layers for simulation.*

| MATERIAL LAYER  |    THICKNESS (mm) |
| --------------- | ----------------- |
| aluminu         |             23.8  |

*Model material parameters.*

| DESCRIPTION | VALUE |
| ----------- | ----- |
| Poisson ratio | 0.33 |
| JC strain coefficient A (MPa) |49|
| JC strain coefficient B (MPa) |157|
| JC strain exponent |0.167|
| JC strain rate coefficient |0.016|
| JC thermal softening |1.7|
| JC reference temperature (K) |293|
| Melt temperature (K) |933|
| Specific heat capacity (J/kg/K) |896|

### Input files.

Simulation setup is written in *asteroid.inp*:
<pre>
------------------- General Model Info ---------------------------------
VERSION               __DO NOT MODIFY__             : 4.1
DIMENSION             dimension of input file       : 2
PATH                  Data file path                : ./
MODEL                 Modelname                     : aluminium_1100_2D
------------------- Mesh Geometry Parameters ---------------------------
GRIDH                 horizontal cells              : 0           : 200         : 50
GRIDV                 vertical cells                : 50          : 240         : 0
GRIDEXT               ext. factor                   : 1.05d0
GRIDSPC               grid spacing                  : 1.5875D-4
CYL                   Cylind. geometry              : 1.0D0
GRIDSPCM              max. grid spacing             : 3.D-3
------------------- Global setup parameters -----------------------------
S_TYPE                setup type                    : DEFAULT
GRAD_TYPE             gradient type                 : NONE
T_SURF                Surface temp                  : 293.D0
------------------- Projectile ("Object") Parameters --------------------
OBJNUM                number of objects             : 1
OBJRESH               CPPR horizontal               : 20
OBJVEL                object velocity               : -7.D3
OBJMAT                object material               : al-1100
OBJTYPE               object type                   : SPHEROID
------------------- Target Parameters ----------------------------------
LAYNUM                layers number                 : 1
LAYPOS                layer position                : 200
LAYMAT                layer material                : al-1100
------------------- Time Parameters ------------------------------------
DT                    initial time increment        : 3.175D-8
DTMAX                 maximum timestep              : 5.D-3
TEND                  end time                      : 8.01D-5
DTSAVE                save interval                 : 1.D-6
------------------- Boundary Condition Parameters ----------------------
BND_L                 left                          : FREESLIP
BND_R                 right                         : FREESLIP
BND_B                 bottom                        : NOSLIP
BND_T                 top                           : OUTFLOW
------------------- Numerical Stability Parameters ---------------------
AVIS                  art. visc. linear             : 0.2D0
AVIS2                 art. visc. quad.              : 1.0D0
------------------- Tracer Particle Parameters -------------------------
TR_QUAL               integration qual.             : 1
TR_SPCH               tracer spacing X              : 1.5875D-4   : 1.5875D-4
TR_SPCV               tracer spacing Y              : 1.5875D-4   : 1.5875D-4
TR_VAR                add. tracer fiels             : #TrP-TrT#
------------------- (Material) Model parameters (global) ---------------
STRESS                Consider stress               : 1
PARTPRES              Pres. in part.                : 1
------------------- Data Saving Parameters -----------------------------
QUALITY               Compression rate              : -50
VARLIST               List of variables             : #Den-Tmp-Pre-Sie-Yld-VEL#
------------------------------------------------------------------------
</pre>

Material parameters used in the model are written in *material.inp*:
<pre>
--------------------------------------------------------
MATNAME    Material name          : al-1100
EOSNAME    EOS name               : aluminu
EOSTYPE    EOS type               : tillo
STRMOD     Strength model         : JNCK
DAMMOD     Damage model           : NONE
ACFL       Acoustic fluidisation  : NONE
PORMOD     Porosity model         : NONE
THSOFT     Thermal softening      : JNCK
LDWEAK     Low density weakening  : NONE
----- Elastic strength parameters ----------------------
POIS       pois                   : 3.3000D-01
----- Minimum Pressure ---------------------------------
PMININ     minimum pressure       : -2.440D+09
----- Thermal parameters -------------------------------
TMELT0     tmelt0                 : 9.3300D+02
ASIMON     a_simon                : 6.0000D+09
CSIMON     c_simon                : 3.0000D+00
----- Johnson-Cook strength parameters -----------------
JC_A       strain coeff. a        : 4.9000D+07
JC_B       strain coeff. b        : 1.5700D+08
JC_N       strain exponent        : 1.6700D-01
JC_C       str. rate coeff c      : 1.6000D-02
JC_M       thermal soft.          : 1.7000D+00
JC_TREF    ref. temperature       : 2.9300D+02
--------------------------------------------------------
</pre>

## Results.

The figure below shows a comparison of iSALE model data with the experimental results from Pierazzo et al. (2008).
![Crater growth](https://isale-code.github.io/images/examples/Aluminum11002D/cratergrowth.png)

The following figures show several timesteps showing the growth of the crater in Al 1100-O.

[[https://isale-code.github.io/images/examples/Aluminum11002D/DenPre00000.png]]

[[https://isale-code.github.io/images/examples/Aluminum11002D/DenPre00003.png]]

[[https://isale-code.github.io/images/examples/Aluminum11002D/DenPre00008.png]]

[[https://isale-code.github.io/images/examples/Aluminum11002D/DenPre00021.png]]

[[https://isale-code.github.io/images/examples/Aluminum11002D/DenPre00033.png]]

[[https://isale-code.github.io/images/examples/Aluminum11002D/DenPre00075.png]]


## References.

Pierazzo E., Artemieva N., Asphaug E., Baldwin E.C., Cazamias J., Coker R., Collins G.S., Crawford D.A., Davison T.M., Elbeshausen D., Holsapple K.A., Housen K.R., Korycansky D G, and Wünnemann K. (2008). Validation of numerical codes for impact and explosion cratering: Impacts on strengthless and metal targets. _Meteoritics and Planetary Science_ *43*:1917-1938.