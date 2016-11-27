# Acoustic-ATC
The code constitutes of four different .edp files:

1. "parameters.eps"

File that contains the physical and geometrical parameters
of the medium where the waves will propagate.
 For each scatterer (circle, kite, or kite2), we have two medium type possibilities:
a layered or in a non-layered one (these can be chosen changing the values of
the string variables 'scatterer' and 'MediumType', respectively).
 Once that both the scatterer and medium type are chosen, one can decide
the (piecewise constant) material properties: mu = rmu + 1.i*imu and eps = rn + 1.i*in,
where the equation considered is div( mu^-1 grad(u)) + k^2 eps u = 0 

This files generates two meshes: the one that "FFback.edp" will use and the one that 
"FFcrack.edp" will use (the background media mesh, and the mesh for the media with a -or a couple 
of- crack).

2. "FFback.edp"
 File that computes the Fourier coefficients of the far-field pattern
associated to the acoustic scattered wave for different incident
plane waves.
 Outputs:
1. The matlab file "filenameBack.m" (filenameBack is a variable that can 
be found in parameters.edp), that contains a Ninc x nbfpro matrix called Aback.
Here Ninc = number of incident waves, nbfpro = truncation level for 
the Fourier series expansion.
2. The matlab file "RHS.m" that contains a Ninc x Nsample matrix called rhs,
where Ninc = number of incident waves, Nsample = number of sample points along
the curve gamma where we will reccord the value of the solution, later used as
a right hand side for the LSM in the crack problem.

3. "FFcrack.edp"
 File that computes the Fourier coefficients of the far-field pattern
associated to the acoustic scattered wave for different incident
plane waves. The medium here is the same as in FFback.edp, except that
there are some (1 or 2) cracks at the interface of two materials.
The 'scatterer' variable in "parameters.edp" corresponds to different geometries
for both the scatterer and the cracks:
circle - Circular scatterer and 1 single crack
kite - kite-shaped scatterer and 1 single crack
kite2 - kite-shaped scatterer and 2 cracks

 Output:
  1. The unique output of "FFcrack.edp" is the matlab file "filenameCrack.m" 
(filenameCrack is a variable that can be found in parameters.edp), that 
contains a Ninc x nbfpro matrix called Adef.
Here Ninc = number of incident waves, nbfpro = truncation level for 
the Fourier series expansion.


4. "auxfunc.edp"
This file contains few auxiliary functions used by "FFback.edp" and "FFcrack.edp":
i) the one that integrates functions in the FE space, against the Fourier basis function on the external circle
(to make a change of basis to Fourier one), and which is very useful in the construction of both the DtN map
and the far-field patterns.
ii) Functions that save the outputs of "FFback.edp" and "FFcrack.edp" as matlab files

