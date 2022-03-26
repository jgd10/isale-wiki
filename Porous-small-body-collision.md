This example is the collision between two dunite planetesimals. This example uses the porosity model, and shows how to setup a non-spherical impactor, and a layered target body.

The impacting body is an oblate spheroid with a semi-major axis of 2.4 km and a semi-minor axis of 1 km. The impact velocity is 5 km/s. The planetesimal moves in a direction parallel to the semi-minor axis. The impactor has a porosity of 40%. The target body is spherical. It has a radius of 5 km. There is a central core of non-porous dunite 2 km in radius. The outer shell is composed of 50% porosity dunite. The dunite in both bodies is represented by the ANEOS equation of state tables. Both bodies have a constant initial temperature of 293K.

## Running the simulation

Go to the relevant example directory
<pre>
cd &lt;prefix&gt;/share/examples/Collision2D
</pre>

Run iSALE2D.  The simulation will take several minutes, so this should be run in the background.
<pre>
./iSALE2D &
</pre>

Now, perform some postprocessing. To produce images of the simulation to visualise pressure and porosity using pySALEPlot: 

<pre>
python Plotting/PrePor.py
</pre>

The images, which should be identical to those shown below, will be output to the directory @PrePor@.

The model can be post-processed to calculate the mass and volume of material shocked to a range of different shock pressures using the command:

<pre>
python Plotting/ShockP.py
</pre>

This will print a table to the screen listing the pressures, the total volume and mass shocked to each pressure, and the volume and mass of each object (impactor, mantle, core) shocked to each pressure. The table for timestep 50 should be the same as the one reproduced in the Results section below. A visual comparison of the shock-processed volumes will also be produced in the `ShockP/` directory (also shown below).

For other examples of how to use pySALEPlot to process this model, see these pySALEPlot example pages: 
* [[psp_plot_arbitrary_number_of_fields|Plot an arbitrary number of fields]]
* [[psp_plot_material|Plot materials]]
* [[psp_plot_material_boundaries|Plot material boundaries]]
* [[psp_plot_tracers|Plot tracers]]
* [[psp_plot_tracer_lines_and_grids|Plot tracer lines/grids]]

## Model parameters summary

*Model parameters for simulation.*

|Description | Value |
| --- | --- |
|Number of high-resolution cells in x-direction  |   280.00 |
|Number of high-resolution cells in y-direction  |   360.00 |
|Cell size in x-direction (m)                    |    40.00 |
|Cell size in y-direction (m)                    |    40.00 |
|Surface temperature (deg. Kelvin)               |   293.00 |
|Gravitational acceleration (m/s$^2$)            |     0.00 |
|>.Projectile Number |  1 |
|Shape                                           |  ELLIPSE |
|Projectile diameter (X-direction) (km)          |     4.80 |
|Projectile diameter (Y-direction) (km)          |     2.00 |
|Projectile velocity (km/s)                      |     5.00 |
|Projectile material (number)                    |  body__1  |
|>.Projectile Number  |  2 |
|Shape                                           |   SPHERE |
|Projectile diameter (km)                        |    10.00 |
|Projectile velocity (km/s)                      |     0.00 |
|Projectile material (number)                    |  mantle2  |
|>.Projectile Number |  3 |
|Shape                                           |   SPHERE |
|Projectile diameter (km)                        |     4.00 |
|Projectile velocity (km/s)                      |     0.00 |
|Projectile material (number)                    |  core__3  |

*Material model parameters*

|Description | body__1| mantle2| core__3 |
| --- | --- | --- | --- |
|Poisson ratio                           | 0.25 |     0.25 |     0.25 |
|Strength at zero pressure (intact; MPa)    |      10. |      10. |      10. |
|Strength at inf. pressure (intact; MPa) |    2000. |    2000. |    2000. |
|Internal friction coeff. (intact)           |     0.60 |     0.60 |     0.60 |
|Strength at zero pressure (damaged; MPa)         |     1.00 |     1.00 |     1.00 |
|Friction coefficient (damaged)                   |     0.60 |     0.60 |     0.60 |
|Tensile strength (MPa)                         |       0. |       0. |       0. |
|Brittle-ductile transition press. (MPa)         |       0. |       0. |       0. |
|Brittle-plastic transition press. (MPa)         |       0. |       0. |       0. |
|Melt Temperature (degrees Kelvin)                |    1373. |    1373. |    1373. |
|Specific Heat Capacity (J/Kg/Kelvin)               |    1000. |    1000. |    1000. |
|Thermal Softening parameter                  |     1.20 |     1.20 |     1.20 |
|Simon parameters for Melt Temp. vs P.             |    1520. |    1520. |    1520. |
|Simon parameters for Melt Temp. vs P.             |     4.05 |     4.05 |     4.05 |
|Initial porosity                         |     0.40 |     0.50 |     0.00 |
|Initial distension                     |     1.67 |     2.00 |     1.00 |
|Distension at onset of crushing              |     1.67 |     2.00 |     1.00 |
|Distension at transition to power-law       |     1.00 |     1.00 |     1.00 |
|Exponential compaction rate              |     0.98 |     0.98 |     0.98 |
|Ratio of porous/nonporous sound speed           |     1.00 |     1.00 |     1.00 |
|Volumetric strain at elastic limit      |   0.00 |     0.00 |     0.00 |
|Volumetric strain at transition         |    -0.51 |    -0.69 |     0.00 |
|Volumetric strain when fully compacted    |    -0.51 |    -0.69 |     0.00 |

h1. Results.

*Shock pressure analysis.* Figures in bold type show the mass of each projectile shock heated to the solidus
For timestep 50 (  5.0003e+00 secs)

|     Pressure|    Total vol|   Total mass|   Impctr Vol|   Mantle Vol|     Core Vol|  Impctr Mass|  Mantle Mass|    Core Mass|
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
|   0.0000e+00|   5.4751e+11|   9.7095e+14|   2.4051e+10|   4.8991e+11|   3.3546e+10|   4.7742e+13|   8.1200e+14|   1.1120e+14|
|   1.0000e+09|   2.1625e+11|   4.1891e+14|   2.4051e+10|   1.6045e+11|   3.1743e+10|   4.7742e+13|   2.6594e+14|   1.0523e+14|
|   2.0000e+09|   1.5287e+11|   3.0557e+14|   2.4028e+10|   1.0209e+11|   2.6747e+10|   4.7695e+13|   1.6922e+14|   8.8663e+13|
|   5.0000e+09|   1.0100e+11|   1.9186e+14|   2.2851e+10|   6.7918e+10|   1.0234e+10|   4.5359e+13|   1.1257e+14|   3.3925e+13|
|   7.8730e+09 (mantle solidus)|   7.8531e+10|   1.4590e+14|   2.1914e+10|   5.1455e+10|   5.1625e+09|   4.3499e+13|   8.5284e+13|   1.7113e+13|
|   1.0000e+10|   6.9601e+10|   1.2785e+14|   2.1089e+10|   4.5145e+10|   3.3660e+09|   4.1862e+13|   7.4826e+13|   1.1158e+13|
|   1.1836e+10 (impactor solidus)|   6.3465e+10|   1.1575e+14|   2.0242e+10|   4.0851e+10|   2.3719e+09|   4.0180e+13|   6.7709e+13|   7.8627e+12|
|   1.5000e+10|   5.1217e+10|   9.2265e+13|   1.5886e+10|   3.4019e+10|   1.3113e+09|   3.1533e+13|   5.6385e+13|   4.3469e+12|
|   2.0000e+10|   1.6414e+10|   2.8811e+13|   2.5284e+09|   1.3417e+10|   4.6888e+08|   5.0187e+12|   2.2238e+13|   1.5543e+12|
|   5.0000e+10|   0.0000e+00|   0.0000e+00|   0.0000e+00|   0.0000e+00|   0.0000e+00|   0.0000e+00|   0.0000e+00|   0.0000e+00|
|   1.0231e+11 (core solidus)|   0.0000e+00|   0.0000e+00|   0.0000e+00|   0.0000e+00|   0.0000e+00|   0.0000e+00|   0.0000e+00|   0.0000e+00|


The shock processed volumes are presented graphically below. This plot is made using the pySALEPlot script `Plotting/ShockP.py`

[[https://isale-code.github.io/images/examples/Collision2D/ShockP-00050.png]]

After 5.0 secs of the model run, a shock pressure analysis reveals that ~84% of the impacting projectile is shock heated to the solidus (a critical shock pressure, P(sol) of 11.8 GPa is required for 40% porosity dunite). This is equivalent to a mass of ~4.02E+13kg. None of the non-porous core of the target body is shock heated to the solidus (P(sol) = 102.3 GPa), but of the 50% porosity shell, ~11% of the material is shock heated to the solidus (P(sol) = 7.9 GPa). This is equivalent to a mass of ~8.52E+13 kg.

The figures below show the pressure and distension in the two colliding planetesimal at several timesteps during the collision. (a) Initial condition. (b) Shock wave propagates through impacting and target bodies. (c) Release wave initiated at back of impacting body. (d) Shock wave propagates through non-porous core. (e) Release wave initiated from back edge of core. (f) High shock pressures released everywhere.

[[https://isale-code.github.io/images/examples/Collision2D/PrePor-00000.png]]
[[https://isale-code.github.io/images/examples/Collision2D/PrePor-00005.png]]
[[https://isale-code.github.io/images/examples/Collision2D/PrePor-00010.png]]
[[https://isale-code.github.io/images/examples/Collision2D/PrePor-00015.png]]
[[https://isale-code.github.io/images/examples/Collision2D/PrePor-00020.png]]
[[https://isale-code.github.io/images/examples/Collision2D/PrePor-00050.png]]