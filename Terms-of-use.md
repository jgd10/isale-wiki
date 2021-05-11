## Access to iSALE

At present, iSALE is not fully open source. It is distributed on a case-by-case basis to academic users in the impact community, strictly for non-commercial use. Scientists interested in using or developing iSALE may apply to use iSALE by email (to isale at imperial.ac.uk), providing the following information.
* Name and institution
* Name of supervisor (for student applicants)
* Email address
* Preferred username
* Date of birth
* Intended use of iSALE (short description)
* Previous experience of numerical modelling and computer operating systems (self or supervisor)
* *Please also cut-and-paste the following paragraph in your application email:*

> I agree to the terms and conditions of iSALE use as described on the iSALE website (http://www.isale-code.de/redmine/projects/isale/wiki/Terms_of_use).

Ongoing access to iSALE is contingent on the following terms:

* iSALE is strictly for non-commercial use
* iSALE accounts are for use only by the registered account holder; redistribution of the code in any part or form is not permitted.
* iSALE comes with absolutely no warranty and no guarantee of support

Failure to comply with any of these terms will result in withdrawal of iSALE access.

> *Please note: Access to the three-dimensional variant "iSALE-3D" is currently restricted to experienced iSALE-2D users who already contributed to the improvement of iSALE (developments, bug-reports, supporting other users)*

## Acknowledging iSALE developers

All users of iSALE are kindly asked to acknowledge the developers of iSALE in any publication (peer-reviewed or otherwise) as a courtesy for the time and effort spent developing and supporting iSALE. Key developers should be named in person.

### iSALE-2D

> We gratefully acknowledge the developers of iSALE-2D, including Gareth Collins, Kai Wünnemann, Dirk Elbeshausen, Tom Davison, Boris Ivanov and Jay Melosh.

### iSALE-3D

> We gratefully acknowledge the developers of iSALE-3D, including Dirk Elbeshausen, Kai Wünnemann, Gareth Collins and Tom Davison.

Where specific modifications have been made by developers for the user's application, it may also be appropriate for an iSALE developer to be named as co-author of any publication resulting from the use of iSALE. Please discuss such matters with the developer that has helped you with your application.

## iSALE description in papers

Due to the long history of iSALE model development and the long list of developers who have made substantial contributions to the functionality of iSALE, we ask that a (very) brief history of iSALE-2D or iSALE-3D is included when describing iSALE in the method section of any manuscript.

### iSALE-2D

For iSALE-2D, this description should include references to these papers: Amsden et al., 1980[1], Wünnemann et al, 2006[2], Collins et al., 2004[3], Ivanov et al., 1997[4], Melosh et al., 1992[5]. For example,

> In this work we use the iSALE-2D shock physics code (Wünnemann et al., 2006), which is based on the SALE hydrocode solution algorithm (Amsden et al, 1980). To simulate hypervelocity impact processes in solid materials SALE was modified to include an elasto-plastic constitutive model, fragmentation models, various equations of state (EoS), and multiple materials (Melosh et al., 1992; Ivanov et al., 1997). More recent improvements include a modified strength model (Collins et al., 2004), a porosity compaction model (Wünnemann et al., 2006; Collins et al., 2011) and a dilatancy model (Collins, 2014). 

A shorter description, appropriate for conference abstracts should still include all key references.

> In this work we use the iSALE shock physics code (Amsden et al, 1980; Collins et al., 2004; Wünnemann et al., 2006).

### iSALE-3D

The development history of iSALE-3D is described in Elbeshausen et al., 2009[7] and Elbeshausen and Wünnemann, 2011[9]. Any description of iSALE-3D should include these references and - if possible - references to papers describing the solution strategy (Hirt et al. 1974[10]) and relevant material models (which are common to iSALE-2D and iSALE-3D): strength model (Collins et al., 2004[3], Ivanov et al., 1997[4], Melosh et al., 1992[5]); porosity model (Wünnemann et al, 2006[2], Collins et al., 2011[6]); dilatancy model (Collins, 2014[14]). For example,

> In this work we use the iSALE-3D shock physics code (Elbeshausen et al., 2009; Elbeshausen and Wünnemann, 2011). This code uses a solver as described in Hirt et al., 1974. The development history of iSALE-3D is described in Elbeshausen et al., 2009. This code includes a strength model (Collins et al., 2004, Melosh et al., 1992; Ivanov et al., 1997) and a porosity compaction model (Wünnemann et al., 2006; Collins et al., 2011).

A shorter description, appropriate for conference abstracts should still include all key references.

> In this work we use the iSALE-3D shock physics code (Elbeshausen et al., 2009; Elbeshausen and Wünnemann, 2011).

In future, we hope that a single authoratitive reference for iSALE will be published, describing all key developments, but until this time we ask users to kindly respect the need for adequate description of iSALE in published works.

### iSALE-Dellen

Since the release of iSALE-Dellen (6/7/2016), two stable versions of iSALE are in use (the previous version was called iSALE-Chicxulub). For this reason, we ask that authors indicate the version of iSALE used in published works (iSALE-Chicxulub or iSALE-Dellen). We have also published the iSALE-Dellen manual on figshare (Collins et al., 2016[15]), which can be cited *in addition to* the references above when describing iSALE-Dellen in scientific articles.

### Validation 

Both hydrocodes have been benchmarked against other hydrocodes (Pierazzo et al., 2008[11]) and validated against experimental data from laboratory scale impacts (Pierazzo et al., 2008[11]; Davison et al, 2011[12], Miljkovic et al., 2012[13]).

## References

[1] Amsden, A., Ruppel, H., and Hirt, C. (1980). SALE: A simplified ALE computer program for fluid flow at all speeds. Los Alamos National Laboratories Report, LA-8095:101p. Los Alamos, New Mexico: LANL.

[2] Wünnemann, K., Collins, G., and Melosh, H. (2006). A strain-based porosity model for use in hydrocode simulations of impacts and implications for transient crater growth in porous targets. Icarus, 180:514--527. "doi":http://dx.doi.org/10.1016/j.icarus.2005.10.013 

[3] Collins, G. S., Melosh, H. J., and Ivanov, B. A. (2004). Modeling damage and deformation in impact simulations. Meteoritics and Planetary Science, 39:217--231. "doi":http://dx.doi.org/10.1111/j.1945-5100.2004.tb00337.x

[4] Ivanov, B. A., Deniem, D., and Neukum, G. (1997). Implementation of dynamic strength models into 2D hydrocodes: Applications for atmospheric breakup and impact cratering. International Journal of Impact Engineering, 20:411--430.

[5] Melosh, H. J., Ryan, E. V., and Asphaug, E. (1992). Dynamic fragmentation in impacts: Hydrocode simulation of laboratory impacts. J. Geophys. Res., 97(E9):14735--14759.

[6] Collins, G., Melosh, H. and Wünnemann, K. (2011). Improvements to the epsilon-alpha porous compaction model for simulating impacts into high-porosity solar system objects. Int. J. Imp. Eng., 38:434-439. "doi":http://dx.doi.org/10.1016/j.ijimpeng.2010.10.013,

[7] Elbeshausen, D., Wünnemann, K., Collins, G.S., (2009) Scaling of oblique impacts in frictional targets: Implications for crater size and formation mechanisms, Icarus, 2009, 204:716-731. "doi":http://dx.doi.org/10.1016/j.icarus.2009.07.018 

[8] Amsden, A.A., Ruppel, H.M., (1981). SALE-3D: A simplified ALE computer program for calculating three-dimensional fluid flow. Los Alamos National Laboratories Report, NUREG/CR-2185;LA-8905:151p. Los Alamos, New Mexico: LANL.

[9] Elbeshausen D. and Wünnemann K. (2011). iSALE-3D: A three-dimensional, multi-material, multi-rheology hydrocode and its applications to large-scale geodynamic processes. In: Schäfer, F. (ed.) ; Hiermaier, S. (ed.): Proceedings of the 11th Hypervelocity Impact Symposium 2010, Freiburg, Germany, April 11-15, 2010. Fraunhofer Verlag, Stuttgart, 828 pp. (Epsilon. Forschungsergebnisse aus der Kurzzeitdynamik, 20) (ISBN 3-8396-0280-7 ; ISBN 978-3-8396-0280-5 ; ISSN 1612-6718)

[10] Hirt, C.W., Amsden, A.A. and Cook, J.L. (1974). An arbitrary Lagrangian-Eulerian computing method for all flow speeds. Journal of Computational Physics, 14(3), pp. 227-253.

[11] Pierazzo, E., Artemieva, N., Asphaug, N., Baldwin, E., Cazamias, E.C., Coker, R., Collins, G.S., Crawford, D.A., Davison, T., Elbeshausen, D., Holsapple, K.A., Housen, K.R.,Korycansky, D.G., Wünnemann, K.,2008. Validation of numerical codes for impact and explosion cratering: impacts on strengthless and metal targets. Meteorit. Planet. Sci. 43, 1917–1938.

[12] Davison, T.M., Collins, G.S., Elbeshausen, D., Wünnemann, K., Kearley, A., 2011. Numerical modeling of oblique hypervelocity impacts on strong ductile targets. Meteorit. Planet. Sci. 46 (10), 1510–1524.

[13] K. Miljković, G. S. Collins, M. R. Patel, D. Chapman, W. Proud (2012), High-velocity impacts in porous solar system materials, AIP Conf. Proc., 1426, 871–874, "doi":http://dx.doi.org/10.1063/1.3686416.

[14] Collins, GS (2014), Numerical simulations of impact crater formation with dilatancy, J. Geophys. Res. Planets, 119, 2600–2619, "doi":http://dx.doi.org/10.1002/2014JE004708.

[15] Collins, G. S., Elbeshausen, D., Davison, T. M.; Wünnemann, K.; Ivanov, B.; Melosh, H. J. (2016): iSALE-Dellen manual. figshare. "doi":https://dx.doi.org/10.6084/m9.figshare.3473690