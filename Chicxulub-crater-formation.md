## Description and instructions.

The model is an attempt to reproduce the Chicxulub crater. It is a low-resolution model of an impact of a 14.4 km diameter asteroid striking a layered target at 12 km/s. The impactor is a sphere of material represented using an ANEOS-derived equation of state table for granite. The target has a surface gravity of 9.81 m/s^2 and comprises 2.8 km sediments (calcite) above 30 km crust (granite), above mantle (dunite). Each material's equation of state is defined using ANEOS-derived tables. Acoustic fluidization (AF) is used to weaken the target and facilitate complex crater collapse. 

The model is similar to those described by Ivanov (2005), Collins et al. (2008) and Christeson et al. (2009), which provided a reasonable fit to observational constraints. This test case model differs because (a) different AF parameters to those used in other models are assigned to the mantle, crust and sediments; and (b) no geotherm is set in this example - the target has a constant temperature of 293K.

## Running the simulation

Go to the relevant example directory
<pre>
cd &lt;prefix&gt;/share/examples/Chicxulub
</pre>

Run iSALE2D.  The simulation will take several hours, so this should be run in the background.
<pre>
./iSALE2D &
</pre>

To produce images of the simulation to visualise the temperature and material movement using pySALEPlot:
<pre>
python Plotting/MatTmp.py
</pre>

The images, which should be identical to those shown below, will be output to the directory `MatTmp/`. The pySALEPlot plotting scripts (see also `<prefix>/share/examples/Chicxulub/Plotting/YldYAc.py`) can easily be modified to generate additional images and analysis.

In addition, this [[psp_plot_vertical_profiles|example script]] plots a vertical profile of pressure at two time steps from the Chicxulub simulation.

## Model parameters summary.

*Model parameters for simulation.*

| DESCRIPTION |                                  VALUE|
| ------------ | ------------------------------------- |
| Number of high-resolution cells in x-direction | 250 |
| Number of high-resolution cells in y-direction | 200 |
| Cell size in x-direction (m)                    | 400 |
| Cell size in y-direction (m)                    | 400 |
| Surface temperature (deg. Kelvin)               | 293 |
| Gravitational acceleration (m/s2)               | 9.81 |
| Projectile diameter (km)                        | 14.4 |
| Projectile velocity (km/s)                      | 12. |
| Projectile material (number)                    | granite |


*Target layers for simulation.*

|MATERIAL LAYER   |    THICKNESS (m)|
| ------------ | ------------------------------------- |
|calcite |             2800.0 |
|granite  |            30000.0|
|dunite_   |           17200.0|


*Material model parameters.*

|DESCRIPTION                               | granite   | dunite_   | calcite|
| ---------------------------------------- | --------- | --------- | ------ |
|Poisson ratio                             | 0.30      | 0.25      | 0.30|
|Strength at zero pressure (intact; MPa)   | 10.       | 10.       | 5.|
|Strength at inf. pressure (intact; MPa)   | 2500.     | 3500.     | 500.|
|Internal friction coeff. (intact)         | 2.00      | 1.20      | 1.|
|Strength at zero pressure (damaged; MPa)  | 0.01      | 0.01      | 0.01|
|Friction coefficient (damaged)            | 0.60      | 0.60      | 0.40|
|Melt Temperature (degrees Kelvin)         | 1673.     | 1373.     | 1500.|
|Specific Heat Capacity (J/Kg/Kelvin)      | 1000.     | 1000.     | 1000.|
|Thermal Softening parameter               | 1.20      | 1.20      | 1.20|
|Simon parameters for Melt Temp. vs P.     | 6000.     | 1520.     | 6000.|
|Simon parameters for Melt Temp. vs P.     | 3.00      | 4.05      | 3.00|
|Visc. of ac. fluid. target (m2/s)         | 288000.   | 2880000.  | 0.|
|Decay time for block oscillations (s)     | 165.60    | 72.00     | 0.|
|A.F. viscosity scaling paramameter        | 0.0080    | 0.080     | 0.|
|A.F. decay time scaling parameter         | 120.      | 500.      | 0.|

## Input files.

Simulation setup is written in `asteroid.inp`:

<pre>
------------------- General Model Info ---------------------------------
VERSION               __DO NOT MODIFY__             : 4.1
DIMENSION             dimension of input file       : 2
PATH                  Data file path                : ./
MODEL                 Modelname                     : Chicxulub
------------------- Mesh Geometry Parameters ---------------------------
GRIDH                 horizontal cells              : 0           : 250         : 60
GRIDV                 vertical cells                : 60          : 200         : 20
GRIDEXT               ext. factor                   : 1.05d0
GRIDSPC               grid spacing                  : 4.D2
CYL                   Cylind. geometry              : 1.0D0
GRIDSPCM              max. grid spacing             : -20.D0
------------------- Global setup parameters -----------------------------
S_TYPE                setup type                    : DEFAULT
T_SURF                Surface temp                  : 293.D0
GRAV_V                gravity                       : -9.81D0
------------------- Projectile ("Object") Parameters --------------------
OBJNUM                number of objects             : 1
OBJRESH               CPPR horizontal               : 18
OBJVEL                object velocity               : -1.2D4
OBJMAT                object material               : granite
OBJDAM                object damage                 : 1.D0
OBJTYPE               object type                   : SPHEROID
------------------- Target Parameters ----------------------------------
LAYNUM                layers number                 : 3
LAYPOS                layer position                : 103         : 178         : 185
LAYMAT                layer material                : dunite_     : granite     : calcite
LAYTPROF              thermal profile               : CONST       : CONST       : CONST
------------------- Time Parameters ------------------------------------
DT                    initial time increment        : 5.0D-3
DTMAX                 maximum timestep              : 5.D-2
TEND                  end time                      : 6.001D2
DTSAVE                save interval                 : 5.D0
------------------- Ac. Fluid. Parameters (see also material.inp) ------
TOFF                  toff                          : 16.D0
CVIB                  c_vib                         : 0.1D0
VIB_MAX               Max. vib.vel.                 : 200.
------------------- Boundary Condition Parameters ----------------------
BND_L                 left                          : FREESLIP
BND_R                 right                         : FREESLIP
BND_B                 bottom                        : NOSLIP
BND_T                 top                           : OUTFLOW
------------------- Numerical Stability Parameters ---------------------
AVIS                  art. visc. linear             : 0.24D0
AVIS2                 art. visc. quad.              : 1.20D0
------------------- Tracer Particle Parameters -------------------------
TR_QUAL               integration qual.             : 1
TR_VAR                add. tracer fiels             : #TrP-TrT#
------------------- Control parameters (global) ------------------------
STRESS                Consider stress               : 1
------------------- Data Saving Parameters -----------------------------
QUALITY               Compression rate              : -50
VARLIST               List of variables             : #Den-Tmp-Pre-Sie-Yld-YAc-Dam-VEL#
------------------------------------------------------------------------
</pre>

Material parameters used in the model are written in `material.inp`:
<pre>
-----------------------------------------------------------------------------
MATNAME    Material name          : granite      : dunite_      : calcite
EOSNAME    EOS name               : granit2      : dunite_      : calcite
EOSTYPE    EOS type               : aneos        : aneos        : aneos
STRMOD     Strength model         : ROCK         : ROCK         : ROCK
DAMMOD     Damage model           : IVANOV       : IVANOV       : IVANOV
ACFL       Acoustic fluidisation  : BLOCK        : BLOCK        : BLOCK
PORMOD     Porosity model         : NONE         : NONE         : NONE
THSOFT     Thermal softening      : OHNAKA       : OHNAKA       : OHNAKA
LDWEAK     Low density weakening  : POLY         : POLY         : POLY
----------------------------------------------------------------------------
POIS       pois                   : 3.0000D-01   : 2.5000D-01   : 3.0000D-01
----------------------------------------------------------------------------
TMELT0     tmelt0                 : 1.6730D+03   : 1.3730D+03   : 1.5000D+03
CHEAT      C_heat                 : 1.0000D+03   : 1.0000D+03   : 1.0000D+03
TFRAC      tfrac                  : 1.2000D+00   : 1.2000D+00   : 1.2000D+00
ASIMON     a_simon                : 6.0000D+09   : 1.5200D+09   : 6.0000D+09
CSIMON     c_simon                : 3.0000D+00   : 4.0500D+00   : 3.0000D+00
----------------------------------------------------------------------------
YDAM0      ydam0 (ycoh)           : 1.0000D+04   : 1.0000D+04   : 1.0000D+04
FRICDAM    fricdam                : 6.0000D-01   : 6.0000D-01   : 4.0000D-01
YLIMDAM    ylimdam                : 2.5000D+09   : 3.5000D+09   : 5.0000D+08
----------------------------------------------------------------------------
YINT0      yint0                  : 1.0000D+07   : 1.0000D+07   : 5.0000D+06
FRICINT    fricint                : 2.0000D+00   : 1.2000D+00   : 1.0000D+00
YLIMINT    ylimint                : 2.5000D+09   : 3.5000D+09   : 5.0000D+08
----------------------------------------------------------------------------
IVANOV_A   Damage parameter       : 1.0000D-04   : 1.0000D-04   : 1.0000D-04
IVANOV_B   Damage parameter       : 1.0000D-11   : 1.0000D-11   : 1.0000D-11
IVANOV_C   Damage parameter       : 3.0000D+08   : 3.0000D+08   : 3.0000D+08
----------------------------------------------------------------------------
GAMETA     gam_eta                : 8.0000D-03   : 8.0000D-02   : 0.0000D-03
GAMBETA    gam_beta               : 1.1500D+02   : 0.5000D+02   : 0.0000D+02
----------------------------------------------------------------------------
</pre>

## Results.

The figures below show a time series of the formation of the Chicxulub crater: (a) at the initial state (b) after 20 s (c) after 80 s (d) after 120 s (e) after 200 s (f) after 600s of the initial impact state. The right panel displays the material type (sediment/crust/mantle); the left side displays the temperature (maximum temperature is 1500K).

[[https://isale-code.github.io/images/examples/Chicxulub/MatTmp-00000.png]]

[[https://isale-code.github.io/images/examples/Chicxulub/MatTmp-00004.png]]

[[https://isale-code.github.io/images/examples/Chicxulub/MatTmp-00016.png]]

[[https://isale-code.github.io/images/examples/Chicxulub/MatTmp-00024.png]]

[[https://isale-code.github.io/images/examples/Chicxulub/MatTmp-00040.png]]

[[https://isale-code.github.io/images/examples/Chicxulub/MatTmp-00120.png]]
