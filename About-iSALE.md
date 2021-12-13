# Introduction to iSALE

*iSALE* (impact-SALE) is a multi-material, multi-rheology shock physics code based on the SALE hydrocode (Simplified Arbitrary Lagrangian Eulerian[1]). iSALE includes extensions, corrections and enhancements to the original SALE code made by several workers since the early 1990s. The original SALE code was capable of simulating only single-material, Newtonian-fluid flow. Melosh[2] began improvements to the code by implementing an elasto-plastic constitutive model in tandem with the viscous model, and incorporated the Grady-Kipp fragmentation algorithm and several equations of state for impacts, including the Tillotson equation of state[3]. Concurrently, Ivanov[4] substantially advanced SALE's underlying solution algorithm by incorporating free-surface and material-interface tracking in Eulerian mode, greatly improved the constitutive model by incorporating (among other things) damage accumulation and strain-weakening, and implemented into the code the semi-analytical equation of state ANEOS[5].  The result of these endeavours was a versatile hydrocode, now known as SALEB[8], capable simulating impact events from first contact of the impactor with the target, to cessation of the final gravity driven collapse of the crater[6].  

Melosh's primarily-Lagrangian version of the original SALE was improved to include a wider range of possible rheologic models (released as SALES-2), and used to simulate impact crater collapse[9]. Wünnemann[10] substantially rewrote large parts of SALE, incorporating the improvements of Ivanov and other advances such as a third target material[11].  Further important refinements to the constitutive model were made by Collins, Melosh and Ivanov[13].  Wünnemann, Collins and Melosh[14] incorporated the ε-α porous-compaction model into iSALE.

More recently, based on previous work of Schmalzl[15], Dirk Elbeshausen implemented in iSALE custom made in-memory compression routines for efficient data output and access.

Thomas Davison and Dirk Elbeshausen improved iSALE's material and tracer particle assignment routines to enable easy set-up of multiple simple-shaped "objects" that can be combined to form complex layered impactor and target bodies.

Gareth Collins added a routine to construct a self-consistent central gravity field for simulation of giant impacts onto spherical planetary bodies.  Collins also made modifications to interface reconstruction method to reduce numerical diffusion of low-volume fraction materials in problems with more than two materials. Collins has also made refinements and improvements to the porous compaction model for simulating impacts in high-porosity target materials[16].

Since 2004, iSALE has been co-developed by Collins and Wünnemann and since 2006 also by Dirk Elbeshausen and Thomas Davison. The software was restructured and rewritten in Fortran 95 by Dirk Elbeshausen. He provided the code with more clearly arranged input-files and enabled an easier usage and extension of the code. Dirk Elbeshausen developed several tools for iSALE, such as a three-dimensional visualization and animation software ([[Vimod_manual|VIMoD]]).

Meanwhile, a three-dimensional version of iSALE is available, developed by Dirk Elbeshausen since 2006[17]. This code also includes a fast and accurate adaptive interface reconstruction algorithm[18] and is parallelized by using Message Passing Interfaces ("MPI":http://www.mcs.anl.gov/research/projects/mpi/).

# Components of the iSALE-code

iSALE is not just a code, physically it is a package comprising different tools, libraries, and programs. The main components of iSALE are briefly described in the following. A more detailed description of the usage of all these programs can be found on separate sites as well as in the manual (PDF) which is contained in the repository.

## iSALE-2D

iSALE (impact-SALE) is a two-dimensional, multi-material, multi-rheology hydrocode. By using either an Eulerian or Lagrangian approach, the code can simulate up to three different materials, plus vacuum, with various strength and damage models. Most recently, a porosity compaction model was added to enable the treatment of porous (sedimentary) rocks.

## iSALE-3D

It has been shown that two-dimensional simulations are indispensable for many different disciplines of geosciences. This is primary due to the low computational costs of those experiments which allow the generation of large parameter studies within a very short time. However, the two-dimensional nature of these codes in general restricts the applicability to simple (axi-symmetric) cases.

With respect to meteorite impacts, two-dimensional simulations are limited to vertical impacts in homogenious targets. More sophisticated scenarios, e.g. oblique impacts or impacts into an irregular topography or stratigraphy, require full three-dimensional simulations. Since these calculations are computationally very expensive, so far no extensive parameter studies have been carried out.

For this purpose we developed iSALE-3D, a three-dimensional, multi-material and multi-rheology hydrocode which is highly optimized and well parallelized.

## iSALE-3D functionality

iSALE-3D (impact-SALE-3D) is a multi-material extension of the SALE3D hydrocode (Simplified Arbitrary Lagrangian Eulerian) and iSALE-2D. This software has been developed and optimised specifically for simulating planetary-scale impact processes. 
The main features are

 * Arbitrary Lagrangian Eulerian (ALE) description of motion
 * Explicit finite-difference/finite-volumes solution algorithm
 * Regular structured mesh
 * Support for multiple-materials
 * Multiple material- and strength-models; calculations of material failure
 * ANEOS and Tillotson equation of state routines
 * Interface reconstruction with different schemes (VOF) available, adaptive scheme selection
 * Artificial viscosity for shock capturing
 * Acoustic fluidization model
 * Fast and efficient in- and output of data by using image compression algorithms
 * Parallelisation using MPI (Message Passing Interface) libraries
 * Comes with a custom 3D-visualization software (VIMoD)

### Validation

iSALE-3D is in the process of being validated against laboratory experiments and has been tested along with other hydrocodes as part of the Impact Hydrocode Benchmark and Validation Project. Model development and validation are ongoing, funded through separate projects, to ensure that iSALE-3D is a state-of-the-art tool in the study of impacts throughout the solar system.
Applications

### Applications

iSALE-3D is being used to study the effect of the impact angle on

 * the size of impact craters
 * the shape of impact craters
 * structural deformations and asymmetries in impact craters
 * the crater formation mechanism and process
 * collisions of small bodies (by our partners at Imperial College)
 * crater formation in high strength targets (by our partners at Imperial College)

Furthermore, iSALE-3D has been used to investigate:

 * the effect of topography on the impact cratering process
 * Landslides; especially the wave characteristics of tsunamigenic rockslides

## pySALEPlot

pySALEPlot is a new plotting tool for iSALE datafiles. The purpose of pySALEPlot is to allow access of the data stored within the iSALE datafiles from within python, so that flexible analyses and plotting can be performed by the user (for example using the matplotlib libraries).

## iSALEPlot

iSALEPlot is a plotting program for visualization and post-processing of data produced by iSALE.  

iSALEPlot is controlled by options in an input file and command line arguments. The primary purpose of iSALEPlot is to visualise iSALE data using 2D contour (colormap) plots or 1D linegraph profiles.  These plots are created by selecting a *Plot type*: a variable label stored by iSALE (e.g., @Den@, @Pre@, etc.).  In addition, by selecting other optional *Plot types* iSALE can be used to perform a number of common post-processing tasks, such as constructing crater profiles, measuring crater dimensions and summing the mass of target and projectile material exposed to different shock pressures.

## VIMoD

Calculations of sophisticated impact scenarios (especially three-dimensional ones) are leading to a huge amount of data. Thus, visualization is not only a useful working step for presenting results. It has now become to a central topic in impact research.

We developed VIMoD (=*V*isualization of *I*mpact *Mo*delling *D*ata), a powerful software which enables a three-dimensional visualization and analysation of modelling data derived from both iSALE and iSALE-3D. VIMoD is completely written in C++. It comes with a Qt-based, user friendly GUI and uses OpenGL to generate the graphics output. The rendered data can be easily rotated or moved. Thus, arbitrary views of the data are possible. VIMoD contains a broad variety of visualization methods (isosurfaces, cutfaces, vectors, tracer and trajectory representations, ...). It enables high-resolution snapshot generation as well as encoding of videos in different formats and qualities. It comes with a plugin-interface which allows to write your own add-ons and thus eases the post-processing of the data.

## iSALEMat

iSALEMat is an assistant for generating material input-files required to start simulations.

## iSALEPar

iSALEPar is an assistant for generating parameter input-files required to start simulations. It accesses a database containing meta-informations about every input-parameter and performs automatic sanity-checks. It helps to find appropriate starting setup-conditions and, thus, eases the familiarization of unexperienced users.

## libjc

libjc is a library containing routines for reading, writing, and checking data.

## ptools/libptools

ptools (libptools.a) is a library containing routines for parsing and editing the input-files.


# Examples

*[Examples for iSALE-Simulations can be found here.](Example-problems)*

# References

[1] Amsden, A., Ruppel, H., and Hirt, C. (1980). SALE: A simplified ALE computer program for fluid flow at all speeds. Los Alamos National Laboratories Report, LA-8095:101p. Los Alamos, New Mexico: LANL.

[2] Melosh, H. J., Ryan, E. V., and Asphaug, E. (1992). Dynamic fragmentation in impacts: Hydrocode simulation of laboratory impacts. J. Geophys. Res., 97(E9):14735--14759.

[3] Tillotson, J. H. (1962). Metallic equations of state for hypervelocity impact. Technical Report GA-3216, General Atomic Report.

[4] Ivanov, B. A., Deniem, D., and Neukum, G. (1997). Implementation of dynamic strength models into 2D hydrocodes: Applications for atmospheric breakup and impact cratering. International Journal of Impact Engineering, 20:411--430. 

[5] Thompson, S. and Lauson, H. (1972). Improvements in the CHART D radiation-hydrodynamic code I I I: revised analytic equations of state. Sandia National Laboratory Report, SC-RR-71 0714:113p.

[6] Ivanov, B. A. and Deutsch, A. (1999). Sudbury impact event: Cratering mechanics and thermal history. In Dessler, B. and Grieve, R. A. F., editors, Large Meteorite Impacts and Planetary Evolution I I, Geological Society of America Special Paper 339, pages 389.

[7] Ivanov, B. A. and Artemieva, N. A. (2002). Numerical modeling of the formation of large impact craters. In Catastrophic Events and Mass Extinctions: Impact and Beyond, Geological Society of Americs Special Paper 356, pages 619--630.

[8] Ivanov, B. A. (2005). Numerical modeling of the largest terrestrial meteorite craters. Solar System Research, 39(5):381-409. 

[9] Collins, G. S., Melosh, H. J., Morgan, J. V., and Warner, M. R. (2002). Hydrocode simulations of Chicxulub crater collapse and peak-ring formation. Icarus, 157:24--33. 

[10] Wünnemann, K. (2002). Numerical modeling of impact-induced modifications of the deep-sea floor. Deep-sea research. Part I, Oceanographic research papers, 49(6):969. 

[11] Wünnemann, K. and Ivanov, B. A. (2003). Numerical modelling of the impact crater depth-diameter dependence in an acoustically fluidized target. Solar System Research, 51(13):831--845.
 
[12] Wünnemann, K., Morgan, J. V., and Jodicke, H. (2005). Is ries crater typical for its size? an analysis based upon old and new geophysical data and numerical modeling. In Kenkmann, T., Horz, F., and Deutsch, A., editors, Large Meteorite Impacts I I I, GSA Special Paper 384, volume 384, pages 67--83. Geol. Soc. Am., Boulder, CO. 

[13] Collins, G. S., Melosh, H. J., and Ivanov, B. A. (2004). Modeling damage and deformation in impact simulations. Meteoritics and Planetary Science, 39:217--231. 

[14] Wünnemann, K., Collins, G., and Melosh, H. (2006). A strain-based porosity model for use in hydrocode simulations of impacts and implications for transient crater growth in porous targets. Icarus, 180:514--527. 

[15] Schmalzl, J. (2003). Using standard image compression algorithms to store data from computational fluid dynamics. Computers & Geosciences, 29(8):1021--1031. doi: DOI: 10.1016/S0098-3004(03)00098-0. 

[16] Collins, G. S., Melosh, H.J. and Wünnemann, K. 2010. Improvements to the epsilon-alpha compaction model for simulating impacts into high-porosity solar system objects, International Journal of Impact Engineering, doi:10.1016/j.ijimpeng.2010.10.013.

[17] Elbeshausen D., Wünnemann K. and Collins G.S. (2009) Scaling of Oblique Impacts in Frictional Targets: Implications for Crater Size and Formation Mechanisms. Icarus 204, 716-731, ISSN: 0019-1035.

[18] Elbeshausen D. and Wünnemann K. (2011). iSALE-3D: A three-dimensional, multi-material, multi-rheology hydrocode and its applications to large-scale geodynamic processes. In: Schäfer, F. (ed.) ; Hiermaier, S. (ed.): Proceedings of the 11th Hypervelocity Impact Symposium 2010, Freiburg, Germany, April 11-15, 2010. Fraunhofer Verlag, Stuttgart, 828 pp.