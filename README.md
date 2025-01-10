## Fortran codes for numerical integral of local terrain effects on various gravity field elements outside geoid
https://www.zcyphygeodesy.com/en/h-nd-125.html
## [Algorithm purpose]
&emsp;```Using the rigorous numerical integral algorithm, from the ground digital elevation model and ground ellipsoidal height grid, compute the local terrain effects on the height anomaly (m), gravity (anomaly/disturbance, mGal), vertical deflection (ʺ, to south, to west) or (disturbing) gravity gradient (E, radial) on or outside the geoid.```  
&emsp;```The normal gravity field is the agreed starting datum for the anomalous gravity field, and there is no terrain effect on the normal gravity field. Therefore, the terrain effects on the gravity, gravity disturbance and  gravity anomaly anywhere are exact equal, that on the geopotential and disturbing geopotential and that on the gravity gradient and disturbing gravity gradient are also equal, espectively.```  
&emsp;```The terrain effect on field element is equal to the negative value of the classic terrain correction, such as the local terrain effect is equal to the negative local terrain correction.```
## [Main program for test entrance]
    Localterrianeffintgrl.f90
    The record format of the input calculation point file: ID (point no / point name), longitude (decimal degrees), latitude (decimal degrees), ellipsoidal height (m)......
    The record format of the output file reslt.txt: Behind the record of the calculation point file, appends 5 columns of local terrain effects on the height anomaly (m), gravity (anomaly/disturbance, mGal), vertical deflection (ʺ, to south, to west) or (disturbing) gravity gradient (E, radial) on or outside the geoid.
## (1) Algorithm module for numerical integral of local terrain effects on various field elements
    LTerAllBLH(BLH,dtm,sfh,nlat,nlon,hd,dr,GRS,ter)
    Input parameters:BLH(3)－longitude (decimal degrees), latitude (decimal degrees), ellipsoidal height (m) of the calculation point.
    Input parameters: dtm(nlat,nlon) - the ground digital elevation model (normal /orthometric height) grid, which is employed to indicate terrain relief.
    Input parameters: sfh(nlat,nlon) - the ground ellipsoidal height grid, which represents the terrian surface position employed to calculate the integral distance.
    Input parameters: dr, hd(6) - the integral radius (m) and grid specification parameters (minimum and maximum longitude, minimum and maximum latitude, longitude and latitude intervals of a cell grid).
    Input parameters: GRS(6) - gm, ae, j2, omega, 1/f, default value
    Return parameters: ter(5) - local terrain effects (in unit of SI) on the height anomaly, gravity (anomaly/disturbance), vertical deflection (to south, to west) or (disturbing) gravity gradient (radial).
## (2) Calculation module for the normal gravity field
    normdjn(GRS,djn); GNormalfd(BLH,NFD,GRS)
    Return parameters: NFD(5) - the normal geopotential (m2/s2), normal gravity (mGal), normal gravity gradient (E), normal gravity line direction (', expressed by its north declination relative to the center of the Earth center of mass) or normal gravity gradient direction (', expressed by its north declination relative to the Earth center of mass).
## (3) Calculation module for Legendre functions and their derivatives to ψ
    LegPn_dt2(pn,dp1,dp2,n,t) ! t=cos ψ
## (4) Algorithm library for transforming of geodetic coordinates
    BLH_RLAT(GRS, BLH, RLAT); BLH_XYZ(GRS, BLH, XYZ)
    RLAT_BLH(GRS, RLAT, BLH)
## (5) Algorithm library for interpolation point value from numerical grid
    CGrdPntD(lon,lat,dt,row,col,hd); CGrdPntD2(lon,lat,dt,row,col,hd)
    CShepard(lon,lat,dt,row,col,hd); Gauss2D(lon,lat,dt,row,col,hd)
## (6) Other auxiliary modules
    PickRecord(str0, kln, rec, nn)
## [For compile and link]
    Fortran90, 132 Columns fixed format. Fortran compiler for any operating system. No external link library required.
## [Algorithmic formula] PAGravf4.5 User Reference https://www.zcyphygeodesy.com/en/
    1.4.1 Format convention for geodetic data file
    7.5.2 Integral formula of local terrain effect outside the Earth
    7.1(4) Low-dgree Legendre function and its first and second derivative algorithms
 
DOS executable test file and all input and output data.
