This is a short demonstration simulation. A 1.6 km diameter impactor strikes a uniform target of the same material at 6.5 km/s; the target and impactor materials are represented using a granite-like material model, including an ANEOS-derived equation of state table and a pressure-, temperature- and damage-dependent strength model; and a constant, spatially uniform Earth-like gravitational acceleration is applied.

## Running the simulation

Go to the relevant example directory
```
cd <prefix>/share/examples/demo2D
```

Run iSALE2D.  The simulation only takes about 30 seconds, so can be run in the foreground
```
./iSALE2D
```

Now, perform some postprocessing. Using pySALEPlot, simply run the plotting script in the example directory:
```
python Plotting/plot.py
```

The images, which should be identical to those shown below, will be output to the directory `Plots/`.  For more information about pySALEPlot scripts useful for visualising this example, see these pages: [[psp_plot_one_field|plotting a field]], [[psp_plot_two_fields|plotting two fields]]. 

Alternatively, to produce similar images using iSALEPlot:
```
./iSALEPlot -f Plotting/iSALEPlot.inp -m demo2D/jdata.dat
```

The images below display the starting simulation conditions (before impact, t=0s), and simulation stills at t=1.2s and t=2.5s. The scalar damage parameter, a measure of the extent of fracturing, is plotted on the right; pressure is shown on the left. The simulation follows the propagation of the shock wave to the edge of the domain and the target fracturing behind the shock. Crater growth has not terminated at the end of the simulation.

[[https://isale-code.github.io/images/examples/demo2D/DamPre-00000.png]]

[[https://isale-code.github.io/images/examples/demo2D/DamPre-00100.png]]

[[https://isale-code.github.io/images/examples/demo2D/DamPre-00200.png]]