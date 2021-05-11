## Post-processing

### Is a way to obtain the state of the particle (i.e., initial position and velocity) at the simulation's end time, when a typical impact scenario is generated (i.e., similar to the case of Chicxulub)?

The fate of material in an Eulerian impact cratering simulation can be recorded by **Tracer Particles**. These are included in the simulation if the option input option `TR_QUAL == 1`. Initial tracer spacing is set by options `TR_SPCH, TR_SPCV` and the field variables to be recorded by the tracers are set by option `TR_VAR` (see the manual or use `./iSALEPar --info [OPTION]` for more information on these options).

If you have used tracers in your simulation, you can interrogate this information using pySALEPlot in post-processing.

Tracer variables are read for each timestep in the same way as fields, e.g.:

```
model = psp.opendatfile('jdata.dat',scale='km')
step = model.readStep(plottype='TrP', timestep=10)
```

will read in the tracer variable "TrP" (Peak Pressure) at timestep 10. Note that the x-y (r-z) position of the tracer is read automatically, whenever you read any tracer variable, so you don't need to read these explicitly.

To access information for a specific tracer, you need to know the tracer ID. One way to determine this number is to use the `findTracer()` function, which is a property of each step and locates the tracer closest to a specified x-y location. For example,

```
tracerID = step.findTracer(5.,-10.)
```

will return the tracer ID number of the tracer that is closest to the point at 5-km radius, and 10-km depth below the surface (at timestep 10). Note that x and y must be specified in the current units (km as specified in the opendatfile command).

To probe the fate of material that originated from a specific location, use `findTracer` at the initial timestep (`timestep=0`); to probe the fate of material that ended up at a specific location, use `findTracer` at the final timestep (`timestep=model.laststep`).

With a known tracer ID, information about the tracer can be accessed with:

```
tracer_radial_position = step.xmark[tracerID] 
tracer_vertical_position = step.ymark[tracerID] 
tracer_pressure = step.TrP[tracerID]
```

where, obviously, only tracer variables that have been stored and read can be accessed.

To generate a time-series of the tracer position, etc., with time, simply loop over the timesteps. For example,

```
tracer_radial_position = []; tracer_vertical_position = []; tracer_pressure = []
for i in range(0,model.nsteps):
    step = model.readStep('TrP',i)
    tracer_radial_position.append(step.xmark[tracerID])
    tracer_vertical_position.append(step.ymark[tracerID])
    tracer_pressure.append(step.TrP[tracerID])
```

Each tracer can be considered to track the parcel of material at its initial location, but the volume and mass of material represented by the tracer is not stored by default. This can be calculated in post-processing, by invoking the `model.tracerMassVol` function. For example, if you run:

```
model.tracerMassVol()
```

after reading the `.dat` file, this generates two arrays `model.tracerVolume` and `model.tracerMass` that specify the volume and mass, respectively, of each tracer.
