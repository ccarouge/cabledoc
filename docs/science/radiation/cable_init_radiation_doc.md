## common_InitRad_coeffs

This subroutine calculates the extinction coefficients for beam radiations and black leaves using equations:

 - eq 13 from Sellers 1985
 - eq B6 from Wang and Leuning, 1998

The same equations are used for the extinction coefficients on all 3 radiation bands used in CABLE.
  
In Wang and Leuning, 1998, these equations are given as:

\[
k_{b}=G_{ross}/\cos \theta
\]

\[
G_{ross}=0.5-(0.633-1.11\cos\theta)\chi-(0.33-0.579\cos\theta)\chi^2
\]

valid for \(-0.4<\chi<0.6\), where:

 - \(\chi\) is an empirical parameter related to the leaf angle distribution and is equal to 0 for a spherical leaf angle distribution.
 - \(\cos\theta\) is the cosine of the sun zenith angle

Where there is no vegetation, ie. the LAI is lower than the threshold, the extinction coefficient, \(k_{b}\) is null.

However, CABLE uses the equivalent form of these equations given by Sellers 1985, eq. 13:

\[
G_{ross} = \phi_{1}+\phi_{2}\cos \theta = (0.5-\chi(0.633+0.33\chi)) + 0.877(1-2\phi_{1})\cos \theta
\]

### Variable equivalence between the equations and CABLE
| CABLE variable  | Equation variable                       |
| --------------- | --------------------------------------- |
| xk (the output) | \(k_{b}\)                               |
| cos3            | \(\cos\theta\)                          |
| xphi1           | \(\phi_{1}=(0.5-\chi(0.633+0.33\chi))\) |
| xphi2           | \(\phi_{2}=(0.877(1-2\phi_{1}))\)       |
| VegXfang        | \(\chi\)                                |

### Proof of the equations equivalence

The 2 equations given for \(G_{ross}\) are equivalent by arthimetic calculation of \(\phi_{2}\).

\[
\phi_{2} = 0.877(1-2\phi_{1})    
\]

\[
\phi_{2} = 0.877-2 \times 0.877(0.5-0.633\chi-0.33\chi^2)    
\]

\[
\phi_{2} = 0.877-0.877+1.754 \times 0.633\chi+1.754 \times 0.33\chi^2)    
\]

\[
\phi_{2} = 1.11\chi+0.579\chi^2    
\]

When replacing \(\phi_{2}\) in \(G_{ross}\):

\[
G_{ross} = \phi_{1} + \phi_{2}\cos\theta = (0.5-\chi(0.633+0.33\chi)) + (1.11\chi+0.579\chi^2)\cos\theta
\]

\[
G_{ross} = 0.5-(0.633-1.11\cos\theta)\chi-(0.33-0.579\cos\theta)\chi^2
\]


