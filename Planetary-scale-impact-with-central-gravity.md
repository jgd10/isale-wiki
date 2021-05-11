## Description and instructions.

The model is a low-resolution model of an impact of a ~200 km diameter asteroid striking the Moon at 12 km/s. The impactor and the mantle of the moon are represented using a dunite material model; the lunar crust is represented by a basalt material model and the lunar core is represented by an iron material model. The gravity field for the moon is computed during start-up to be thermodynamically self-consistent with the pressure, density and temperature of the Moon's interior. Each material's equation of state is defined using ANEOS-derived tables. Acoustic fluidization (AF) is used to weaken the target and facilitate complex crater collapse, although on this scale its role is minor. The simulation terminates at the end of the excavation stage; to simulate the collapse stage as well users should extend the simulation time to approximately 7200 seconds (2 hours).

The example demonstrates how to set-up iSALE for 2D central gravity problems involving a layered target planet.

## Running the simulation

Go to the relevant example directory
<pre>
cd <prefix>/share/examples/Planet2D
</pre>

Run iSALE2D.  The simulation takes about half an hour, so this should be run in the background.
<pre>
./iSALE2D &
</pre>

## Model parameters summary.


*Model parameters for simulation.*

| DESCRIPTION |                                  VALUE|
| --- | --- |
| Number of high-resolution cells in x-direction | 180 |
| Number of high-resolution cells in y-direction | 420 |
| Cell size in x-direction (km)                    | 10 |
| Cell size in y-direction (km)                    | 10 |
| Surface temperature (deg. Kelvin)               | 293 |
| Gravitational acceleration (m/s2)               | C.G. |
| Projectile diameter (km)                        | 200 |
| Projectile velocity (km/s)                      | 12. |
| Projectile material (number)                    | mantle_ |


*Target layers for simulation.*

|MATERIAL LAYER   |    Radius (km)|
| --- | --- |
|crust__ |             1750 |
|mantle_ |             1700 |
|core___ |              350 |


*Material model parameters.*

|DESCRIPTION                               | crust__   | mantle_   | core___|
| --- | --- | --- | --- |
|Poisson ratio                             | 0.30      | 0.25      | 0.30|
|Strength at zero pressure (intact; MPa)   | 10.       | 10.       | 100.|
|Strength at inf. pressure (intact; MPa)   | 3500.     | 3500.     | 0.00|
|Internal friction coeff. (intact)         | 1.20      | 1.20      | 0.00|
|Strength at zero pressure (damaged; MPa)  | 0.01      | 0.01      | 0.00|
|Friction coefficient (damaged)            | 0.60      | 0.60      | 0.00|
|Melt Temperature (degrees Kelvin)         | 1393.     | 1373.     | 1811.|
|Specific Heat Capacity (J/Kg/Kelvin)      | 1094.     | 1217.     | 451.|
|Thermal Softening parameter               | 1.20      | 1.20      | 1.20|
|Simon parameters for Melt Temp. vs P.     | 6000.     | 1520.     | 107000.|
|Simon parameters for Melt Temp. vs P.     | 3.00      | 4.05      | 1.76|
|A.F. viscosity scaling paramameter        | 0.0080    | 0.080     | 0.|
|A.F. decay time scaling parameter         | 120.      | 500.      | 0.|

## Results.

### Post-processing instructions

To produce images of the simulation using pySALEPlot:
<pre>
python Plotting/MatDamDenTmp.py
</pre>
The images, which should be the same as those shown below, will be output to the directory `Plots/`.

Finally, you can compare the starting conditions for your model with benchmark data using:
<pre>
python Plotting/plot.py
</pre>

This produces a PDF image: `Planet2D_Profile.pdf`

The figures below show a time series of the formation of the crater: (a) at the initial state (b) after 1 min (c) after 2 mins (d) after 5 mins (e) after 10 mins. From left to right, the panels display the material type (crust/mantle/core); damage, density and temperature.

[[https://isale-code.github.io/images/examples/Planet2D/00000.png]]

[[https://isale-code.github.io/images/examples/Planet2D/00012.png]]

[[https://isale-code.github.io/images/examples/Planet2D/00024.png]]

[[https://isale-code.github.io/images/examples/Planet2D/00060.png]]

[[https://isale-code.github.io/images/examples/Planet2D/00120.png]]

