This numerical model shows a vertical impact into sand under very high gravity (500G). A spherical polyethylene projectile, 13 mm in diameter, impacts at 1.9 km/s into sand, which is represented in the model as 44% porous fused silica. The impact conditions replicate those of impact experiments into sand in a centrifuge by Housen and Holsapple (2003). 

## Running the simulation

Change into the relevant example directory and run the problem in the background. The calculation should take a few hours.

<pre>
cd &lt;prefix&gt;/share/examples/Sand2D
./iSALE2D &
</pre>

## Problem description.

This example demonstrates the use of epsilon-alpha porosity model (`PORMOD==WUNNEMA`), which calculates the compaction of pore space between sand grains. For more details see the manual and: Wunnemann et al. (2006), Collins et al. (2011), Miljkovic et al. (2012). 

### Material parameters summary.

The epsilon-alpha porosity model (`PORMOD==WUNNEMA`) is used in conjunction with a simple stiffened-gas equation of state for solid fused silica (parameters from Borg et al., 2005), named in material.inp as `fuseqtz`. 

<pre>
PORMOD     Porosity model         : WUNNEMA
--------------- Porosity properties -------------
</pre>
`ALPHA0` sets the initial distension, which is related to initial porosity by porosity = 1.-1./alpha = 0.44444
<pre>
ALPHA0  Initial porosity          : 1.80D0   
</pre>
`EPSE0` sets the volume strain threshold for elastic compaction. As this is zero, the material will begin compacting with any increase in pressure
<pre>
EPSE0   Elastic threshold         : 0.00D0
</pre>
`ALPHAX` sets the distension at which the crush curve switches from exponential to power-law (see Wunnemann et al. (2006) and Collins et al. (2011) for details).
<pre>
ALPHAX  Transition                : 1.29D0
</pre>
`KAPPA` sets the rate at which compaction occurs with increasing volume strain; 0.97-0.98 is typical for sand, see Wunnemann et al. (2006)
<pre>
KAPPA   Exp coefficient           : 0.988D0
</pre>
`CHI` is the ratio of the bulk sound speeds of the initial porous material and the non-porous matrix material (fused silica), see Collins et al. (2011). 
<pre>
CHI     Sound speed ratio         : 0.33D0
-------------------------------------------------
</pre>

### Input files.

Mesh includes high resolution zone and an extension zones. The cell size is such that the size of the mesh correspond to laboratory scale experiments. 

<pre>
------------------- Mesh Geometry Parameters ---------------------------------------
GRIDH                 horizontal cells              : 0           : 150         : 45
GRIDV                 vertical cells                : 60          : 200         : 0
GRIDEXT               ext. factor                   : 1.05d0
GRIDSPC               grid spacing                  : 5.0D-4
</pre>

To simulate the conditions in the laboratory centrifuge, the (constant) vertical gravity is set to nearly 500 G:

<pre>
GRAV_V                gravity                       : -4.905D3
</pre>

Two important parameters in this set up are `DTMAX` and `ANC`:

<pre>
------------------- Time Parameters ---------------------------------
DTMAX                 maximum timestep              : 5.0D-8
------------------- Numerical Stability Parameters ------------------
ANC                   alt. node coupl.              : 0.4D0
</pre>

In this context, `ANC` is used to suppress spurious deformation along the symmetry axis by activating the alternate node coupler in cells close to the left boundary.

The magnitude of the coupler `anco` is proportional to the timestep `dt`, normalised by the input parameter `DTMAX`: `anco = ANC*dt/DTMAX`. Hence, if `DTMAX` is set to be too large, the alternate node coupler will have no effect.  Hence, in this simulation `DTMAX` has been carefully chosen to be approximate twice the maximum timestep actually used in the calculation (recorded in `PROGRESS/timestep.txt0`). This is so that the value of `anco` during most of the simulation is ~0.4/2 = 0.2, and is less if the timestep is smaller.

## Post-processing and results.

To produce output images using pySALEPlot:
<pre>
python Plotting/plot.py
</pre>
This produces a series of images in the directory `Plots/`, two of which are shown below.  The plots show distension (left) and porosity (right) at 0, 0.5, 2.5 ms and 5 ms after impact. The simulation ends after 5 ms (`TEND`=5 ms in the example `asteroid.inp` file); however, the crater in sand is not fully formed at this time--extending the end time is required to simulate crater formation until completion.

[[https://isale-code.github.io/images/examples/Sand2D/00000.png]]

[[https://isale-code.github.io/images/examples/Sand2D/00010.png]]

[[https://isale-code.github.io/images/examples/Sand2D/00050.png]]

[[https://isale-code.github.io/images/examples/Sand2D/00100.png]]